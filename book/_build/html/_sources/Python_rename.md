# Author and Date Block

```python
import os
from datetime import date

def add_metadata(file_path, author, date_edited):
    with open(file_path, 'r') as file:
        lines = file.readlines()

    # Find the first heading (starts with '# ') and insert metadata after it
    for i, line in enumerate(lines):
        if line.startswith('# '):
            lines.insert(i+1, f"\n:::{'{card}'}\n**Authors:** {author}\n\n**Last Edited:** {date_edited}\n:::\n\n")
            break

    with open(file_path, 'w') as file:
        file.write(''.join(lines))

def process_directory(root_dir, author, date_edited):
    for root, dirs, files in os.walk(root_dir):
        for file in files:
            if file.endswith('.md'):
                file_path = os.path.join(root, file)
                add_metadata(file_path, author, date_edited)
        dirs.sort()  # process directories in sorted order

root_dir = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/'
author = 'Your Name'
date_edited = date.today().isoformat()
process_directory(root_dir, author, date_edited)

```


# Formatting Tags

```python
import os
import re

def process_file(file_path):
    with open(file_path, 'r') as file:
        lines = file.readlines()

    with open(file_path, 'w') as file:
        for line in lines:
            tag_line = re.match(r'Tags: (.*)', line)
            if tag_line:
                tags = tag_line.group(1).split(', ')
                tags = [tag.replace(' ', '-') for tag in tags]
                new_tag_line = ', '.join(tags)
                line = f"```{{tags}} {new_tag_line}\n```\n"
            file.write(line)

def process_directory(root_dir):
    for root, dirs, files in os.walk(root_dir):
        for file in files:
            if file.endswith('.md'):
                file_path = os.path.join(root, file)
                process_file(file_path)
        dirs.sort()  # process directories in sorted order

root_dir = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/test'
process_directory(root_dir)

```


# Creating Dropdown

```python
import os
import re

def replace_dropdown_pattern_in_file(md_file):
    with open(md_file, 'r') as file:
        lines = file.readlines()

    with open(md_file, 'w') as file:
        i = 0
        while i < len(lines):
            if re.match("^- .+", lines[i].strip()):
                title = lines[i].strip().lstrip("- ")
                content = []
                while i+1 < len(lines) and (lines[i+1].strip() == "" or re.match("^\s+.+", lines[i+1])):
                    content.append(lines[i+1].strip())
                    del lines[i+1]

                content_str = '\n'.join(content)
                new_block = f":::{{dropdown}} {title}\n\n{content_str}\n:::\n"
                lines[i] = new_block

            i += 1
        file.write(''.join(lines))

def process_directory(root_dir):
    for root, dirs, files in os.walk(root_dir):
        for file in files:
            if file.endswith('.md'):
                md_file = os.path.join(root, file)
                replace_dropdown_pattern_in_file(md_file)
        dirs.sort()  # process directories in sorted order

root_dir = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/'
process_directory(root_dir)
```


# Create boxes for "<aside"

```python
import os
import re

def replace_aside_tags_in_file(md_file):
	with open(md_file, 'r') as file:
		content = file.read()

	with open(md_file, 'w') as file:
		updated_content = re.sub(r"<aside>", ":::{card}", content)
		updated_content = re.sub(r"</aside>", ":::", updated_content)
		file.write(updated_content)

def process_directory(root_dir):
	for root, dirs, files in os.walk(root_dir):
		for file in files:
			if file.endswith('.md'):
				md_file = os.path.join(root, file)
				replace_aside_tags_in_file(md_file)
		dirs.sort()  # process directories in sorted order

root_dir = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course'
process_directory(root_dir)

```


# Fix headers depth

```python
import os
import re

def increase_header_depth_in_file(md_file):
	with open(md_file, 'r') as file:
		lines = file.readlines()

	with open(md_file, 'w') as file:
		first_header = True
		for line in lines:
			if re.match("^#+ ", line):
				if first_header:
					first_header = False
				else:
					line = "#" + line
			file.write(line)

def process_directory(root_dir):
	for root, dirs, files in os.walk(root_dir):
		for file in files:
			if file.endswith('.md'):
				md_file = os.path.join(root, file)
				increase_header_depth_in_file(md_file)
		dirs.sort()  # process directories in sorted order

root_dir = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course'
process_directory(root_dir)

```


# Making sphinx cards overview pages

```python
import os
from PIL import Image

def create_sphinx_card(root_dir):
	with open(os.path.join(root_dir, '!index.md'), 'w') as index_file:
		index_file.write(f"# {root_dir.split('/')[-1].replace('_', ' ')}\n\n")
		index_file.write(":::::{grid} 1 1 2 3\n")
		index_file.write(":class-container: text-center\n")
		index_file.write(":gutter: 3\n\n")

		for item in sorted(os.listdir(root_dir)):
			item_path = os.path.join(root_dir, item)
			if os.path.isdir(item_path):
				print(f"Processing directory: {item}")
				# find the image for the card
				image = None
				for sub_item in sorted(os.listdir(item_path)):
					print(f"Checking sub-item: {sub_item}")
					if sub_item.lower().endswith(('.png', '.jpg', '.jpeg')):
						print(f"Found image: {sub_item}")
						image = sub_item
						img = Image.open(os.path.join(item_path, image))
						width, height = img.size
						new_size = min(width, height)
						left = (width - new_size)/2
						top = (height - new_size)/2
						right = (width + new_size)/2
						bottom = (height + new_size)/2
						img = img.crop((left, top, right, bottom))
						img.save(os.path.join(item_path, "cover" + os.path.splitext(image)[1]))
						break

				if image is not None:
					index_file.write(":::{grid-item-card}\n")
					index_file.write(f":link: {item}/!index\n")
					index_file.write(":link-type: doc\n")
					index_file.write(f":img-top: {item}/cover{os.path.splitext(image)[1]}\n")  # Change the image filename here
					index_file.write(":class-header: bg-light\n\n")

					index_file.write(f"{item.replace('_', ' ')}\n\n^^^\ninsert summary here\n\n")

					index_file.write(":::\n")

root_dir = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Knowledge_base/Graduation_Projects'
create_sphinx_card(root_dir)
```


# removes icons, parenthesis, and spaces also renames the markdown links

```python

import os
import re

def remove_non_ascii(string):
    return ''.join(i for i in string if ord(i)<128)

def replace_special_chars(string):
    return string.replace(' ', '_').replace('(', '_').replace(')', '_')

def update_markdown_links(root_dir):
    for dirpath, dirnames, filenames in os.walk(root_dir):
        for filename in filenames:
            if filename.endswith('.md'):
                with open(os.path.join(dirpath, filename), 'r+') as md_file:
                    content = md_file.read()

                    links = re.findall(r'\[(.*?)\]\((.*?)\)', content)

                    for link in links:
                        old_text, old_path = link
                        new_text = remove_non_ascii(old_text)
                        new_path = replace_special_chars(remove_non_ascii(old_path))
                        content = content.replace(old_text, new_text).replace(old_path, new_path)
                    md_file.seek(0)
                    md_file.write(content)
                    md_file.truncate()

def rename_files_and_folders(root_dir):
    for dirpath, dirnames, filenames in os.walk(root_dir):
        # rename folders

        for dirname in dirnames:
            new_dirname = replace_special_chars(remove_non_ascii(dirname))
            old_dir_name = os.path.join(dirpath, dirname)
            new_dir_name = os.path.join(dirpath, new_dirname)
            os.rename(old_dir_name, new_dir_name)

        # rename files

        for filename in filenames:
            new_filename = replace_special_chars(remove_non_ascii(filename))
            old_file_name = os.path.join(dirpath, filename)
            new_file_name = os.path.join(dirpath, new_filename)
            os.rename(old_file_name, new_file_name)

root_dir = @vault_path

rename_files_and_folders(root_dir)

update_markdown_links(root_dir)

```

# youtube iframes


```python

import os
import re

def replace_youtube_links(root_dir):
    # Regex pattern to match YouTube URLs
    pattern = r'(https?://(?:www\.)?(?:youtube\.com/watch\?v=|youtu\.be/)([A-Za-z0-9_-]{10}[A-Za-z0-9_-]{1}))'
    
    for dirpath, _, filenames in os.walk(root_dir):
        # Check only markdown files

        for filename in [f for f in filenames if f.endswith(".md")]:
            file_path = os.path.join(dirpath, filename)
            with open(file_path, 'r+') as f:
                content = f.read()

                # Find YouTube URLs and replace with iframe embed link

                content_new = re.sub(pattern, r'<iframe width="560" height="315" src="https://www.youtube.com/embed/\2" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>', content)

                # If content has changed, write it back to the file

                if content != content_new:
                    f.seek(0)
                    f.write(content_new)
                    f.truncate()

root_dir = @vault_path

replace_youtube_links(root_dir)

```

# Turn single linebreaks into double line breaks

```python
import os
import re

def is_inside_code_block(line, is_in_block):
    if line.strip().startswith('```'):
        is_in_block = not is_in_block
    return is_in_block

def double_linebreaks(root_dir):
    for dirpath, _, filenames in os.walk(root_dir):
        for filename in filenames:
            if filename.endswith('.md'):
                filepath = os.path.join(dirpath, filename)
                with open(filepath, 'r') as md_file:
                    lines = md_file.readlines()

                new_lines = []
                is_in_block = False
                for line in lines:
                    is_in_block = is_inside_code_block(line, is_in_block)
                    if not is_in_block and line == "\n":
                        new_lines.append("\n")
                    new_lines.append(line)

                with open(filepath, 'w') as md_file:
                    md_file.writelines(new_lines)

root_dir = '/path/to/your/directory'
double_linebreaks(root_dir)
```



# Remove [********************]


```python
import os
import re

def boldify_text(root_dir):
    for dirpath, _, filenames in os.walk(root_dir):
        for filename in filenames:
            if filename.endswith('.md'):
                filepath = os.path.join(dirpath, filename)
                with open(filepath, 'r+') as md_file:
                    content = md_file.read()
                    content = re.sub(r"\*{3,}(.*?)\*{3,}", r"**\1**", content)
                    md_file.seek(0)
                    md_file.write(content)
                    md_file.truncate()

root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course"

boldify_text(root_dir)
```


# Make sphinx cards

```python
import os

def create_sphinx_card(root_dir):
    with open(os.path.join(root_dir, '!index.md'), 'w') as index_file:
        index_file.write(f"# {root_dir.split('/')[-1].replace('_', ' ')}\n\n")
        index_file.write(":::::{grid} 1 1 2 3\n")
        index_file.write(":class-container: text-center\n")
        index_file.write(":gutter: 3\n\n")
                

        for item in os.listdir(root_dir):
            item_path = os.path.join(root_dir, item)
            if os.path.isdir(item_path):
                # find the image for the card
                image = None
                for sub_item in os.listdir(item_path):
                    if sub_item.lower().endswith(('.png', '.jpg')):
                        image = sub_item
                        if sub_item.lower() == 'cover.png' or sub_item.lower() == 'cover.jpg':
                            break
                if image is None:
                    continue

                index_file.write(":::{grid-item-card}\n")
                index_file.write(f":link: {item}/!index\n")
                index_file.write(":link-type: doc\n")
                index_file.write(f":img-top: {item}/{image}\n")
                index_file.write(":class-header: bg-light\n\n")

                index_file.write(f"{item.replace('_', ' ')}\n\n^^^\ninsert summary here\n\n")
                index_file.write(":::\n")

root_dir = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Knowledge_base/Graduation_Projects'
create_sphinx_card(root_dir)
```


# made with chatgpt

```python

import os

def rename_files_and_folders(root_dir):

    for dirpath, dirnames, filenames in os.walk(root_dir):

        # rename folders

        for i in range(len(dirnames)):

            old_dir_name = os.path.join(dirpath, dirnames[i])

            new_dir_name = os.path.join(dirpath, dirnames[i].replace(' ', '_'))

            os.rename(old_dir_name, new_dir_name)

        # rename files

        for i in range(len(filenames)):

            old_file_name = os.path.join(dirpath, filenames[i])

            new_file_name = os.path.join(dirpath, filenames[i].replace(' ', '_'))

            os.rename(old_file_name, new_file_name)

# replace with the root directory you want to start renaming from

root_dir = @vault_path

rename_files_and_folders(root_dir)

```


```python

print("Vault path:", @vault_path)

print("Vault url:", @vault_url)

print("Note path:", @note_path)

print("Note url:", @note_url)

print("Note title:", @title)

```



renames the files properly and updates links

needs to be run multiple times and open up the folders multiple times too

```python 

import os

import re

def rename_files_and_folders(root_dir):

    for dirpath, dirnames, filenames in os.walk(root_dir):

        # rename folders

        for dirname in dirnames:

            old_dir_name = os.path.join(dirpath, dirname)

            new_dir_name = os.path.join(dirpath, dirname.replace(' ', '_'))

            os.rename(old_dir_name, new_dir_name)

        # rename files and update links in markdown files

        for filename in filenames:

            old_file_name = os.path.join(dirpath, filename)

            new_file_name = os.path.join(dirpath, filename.replace(' ', '_'))

            os.rename(old_file_name, new_file_name)

            # check if file is markdown

            if new_file_name.endswith(".md"):

                with open(new_file_name, 'r+') as f:

                    content = f.read()

                    # regex pattern for markdown links

                    pattern = r'\[([^\]]+)\]\(([^\)]+)\)'

                    matches = re.findall(pattern, content)

                    for match in matches:

                        old_link = match[1]

                        new_link = old_link.replace('%20', '_')

                        content = content.replace(old_link, new_link)

                    # write the updated content back to the file

                    f.seek(0)

                    f.write(content)

                    f.truncate()

root_dir = @vault_path

rename_files_and_folders(root_dir)

```

# youtube iframes

```python

import os

import re

def replace_youtube_links(root_dir):

    # Regex pattern to match YouTube URLs

    pattern = r'(https?://(?:www\.)?(?:youtube\.com/watch\?v=|youtu\.be/)([A-Za-z0-9_-]{10}[A-Za-z0-9_-]{1}))'

    for dirpath, _, filenames in os.walk(root_dir):

        # Check only markdown files

        for filename in [f for f in filenames if f.endswith(".md")]:

            file_path = os.path.join(dirpath, filename)

            with open(file_path, 'r+') as f:

                content = f.read()

                # Find YouTube URLs and replace with iframe embed link

                content_new = re.sub(pattern, r'<iframe width="560" height="315" src="https://www.youtube.com/embed/\2" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>', content)

                # If content has changed, write it back to the file

                if content != content_new:

                    f.seek(0)

                    f.write(content_new)

                    f.truncate()

root_dir = @vault_path

replace_youtube_links(root_dir)

```

# trying to remove emojis

```python

import os

def remove_non_ascii(string):

    return ''.join(i for i in string if ord(i)<128)

def replace_special_chars(string):

    return string.replace(' ', '_').replace('(', '_').replace(')', '_')

def rename_files_and_folders(root_dir):

    for dirpath, dirnames, filenames in os.walk(root_dir):

        # rename folders

        for dirname in dirnames:

            new_dirname = replace_special_chars(remove_non_ascii(dirname))

            old_dir_name = os.path.join(dirpath, dirname)

            new_dir_name = os.path.join(dirpath, new_dirname)

            os.rename(old_dir_name, new_dir_name)

        # rename files

        for filename in filenames:

            new_filename = replace_special_chars(remove_non_ascii(filename))

            old_file_name = os.path.join(dirpath, filename)

            new_file_name = os.path.join(dirpath, new_filename)

            os.rename(old_file_name, new_file_name)

root_dir = @vault_path

rename_files_and_folders(root_dir)

```

