
# Auto-generate table of contents from scratch saved as _toctest.yml')

```python
import os

def get_dirs(root_dir):
    dir_list = [d for d in os.listdir(root_dir) if os.path.isdir(os.path.join(root_dir, d))]
    return sorted(dir_list, key=str.casefold)

def generate_toc(root_dir, root_path):
    toc = []
    toc.append("# Table of contents")
    toc.append("# Learn more at https://jupyterbook.org/customize/toc.html\n")
    toc.append("format: jb-book")
    toc.append(f"root: {root_path}/intro.md\n")
    toc.append("chapters:")

    for d in get_dirs(root_dir):
        toc.append(f"- file: {root_path}/{d}/!index.md")
        toc.append("  sections:")

        sub_dir = os.path.join(root_dir, d)
        for sub_d in get_dirs(sub_dir):
            toc.append(f"    - file: {root_path}/{d}/{sub_d}/!index.md")
            if get_dirs(os.path.join(sub_dir, sub_d)):
                toc.append("      sections:")
                sub_sub_dir = os.path.join(sub_dir, sub_d)
                for sub_sub_d in get_dirs(sub_sub_dir):
                    toc.append(f"      - file: {root_path}/{d}/{sub_d}/{sub_sub_d}/!index.md")
    
    toc.append(f"- file: _tags/tagsindex.md")

    return toc

def write_toc_to_file(toc, filename="_toctest.yml"):
    # Replace '/path/to/directory' with the actual path where you want to save the file
    full_path = os.path.join(save_path, filename)
    with open(full_path, 'w') as f:
        f.write('\n'.join(toc))

save_path = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/'
root_dir = '/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course'
root_path = "Grasshopper_Rhino_course"
toc = generate_toc(root_dir, root_path)
write_toc_to_file(toc, '_toctest.yml')

```

# Making sphinx cards overview pages

```python
import os
import re
from PIL import Image

def create_sphinx_card(root_dir):
    title = os.path.basename(root_dir).replace('_', ' ')
    with open(os.path.join(root_dir, '!index.md'), 'w') as index_file:
        index_file.write(f"# {title}\n\n")
        index_file.write(":::::{grid} 1 1 2 3\n")
        index_file.write(":class-container: text-center\n")
        index_file.write(":gutter: 3\n\n")

        for item in sorted(os.listdir(root_dir)):
            item_path = os.path.join(root_dir, item)
            if os.path.isdir(item_path):
                print(f"Processing directory: {item}")

                # Extract the title from the markdown file
                md_file_path = os.path.join(item_path, '!index.md')
                if os.path.isfile(md_file_path):
                    with open(md_file_path, 'r', encoding='utf-8') as md_file:  # specify the encoding
                        md_content = md_file.read()
                    # Search for the first Heading 1
                    match = re.search(r'^#\s*(.*)$', md_content, re.MULTILINE)
                    if match:
                        card_title = match.group(1)
                    else:
                        card_title = item.replace('_', ' ')  # Use the folder name as the fallback title
                else:
                    continue  # Skip this folder if no markdown file is found

                # Check for existing cover image
                cover_image = None
                for sub_item in sorted(os.listdir(item_path)):
                    if 'cover' in sub_item.lower() and sub_item.lower().endswith(('.png', '.jpg', '.jpeg')):
                        cover_image = sub_item

                target_aspect = 16/9
                if cover_image:
                    # If cover image exists, open it, check aspect ratio and modify if necessary
                    img = Image.open(os.path.join(item_path, cover_image)).convert('RGB')  # convert image to RGB mode
                    width, height = img.size
                    aspect = width / height
                    if aspect != 16/9:  # Check if the image has a 16:9 aspect ratio
                        # Get the current aspect ratio
                        if aspect > target_aspect:
                            # If the original aspect ratio is greater than 16:9, crop the image
                            new_width = int(height * target_aspect)
                            left = (width - new_width) / 2
                            right = (width + new_width) / 2
                            img = img.crop((left, 0, right, height))
                        elif aspect < target_aspect:
                            # If the original aspect ratio is less than 16:9, pad the image
                            new_height = int(width / target_aspect)
                            top = (height - new_height) / 2
                            bottom = (height + new_height) / 2
                            img = img.crop((0, top, width, bottom))

                        cover_image = "cover_crop" + os.path.splitext(cover_image)[1]  # update cover_image variable
                        img.save(os.path.join(item_path, cover_image))

                # ... (rest of the code)
                # I've omitted the rest of the code to keep this response concise, but the indentation should remain consistent.

                else:
                    # If no cover image exists, create one from the first image found
                    for sub_item in sorted(os.listdir(item_path)):
                        if sub_item.lower().endswith(('.png', '.jpg', '.jpeg')):
                            img = Image.open(os.path.join(item_path, sub_item)).convert('RGB')  # convert image to RGB mode
                            width, height = img.size
                            # Get the current aspect ratio
                            aspect = width / height
                            if aspect > target_aspect:
                                # If the original aspect ratio is greater than 16:9, crop the image
                                new_width = int(height * target_aspect)
                                left = (width - new_width) / 2
                                right = (width + new_width) / 2
                                img = img.crop((left, 0, right, height))
                            elif aspect < target_aspect:
                                # If the original aspect ratio is less than 16:9, pad the image
                                new_height = int(width / target_aspect)
                                top = (height - new_height) / 2 
                                bottom = (height + new_height) / 2 
                                img = img.crop((0, top, width, bottom))
	                            
                            cover_image = "cover_crop" + os.path.splitext(sub_item)[1]
                            img.save(os.path.join(item_path, cover_image))
                            break

                if cover_image is not None:
                    index_file.write(":::{grid-item-card}\n")
                    index_file.write(f":link: {item}/!index\n")
                    index_file.write(":link-type: doc\n")
                    index_file.write(f":img-top: {item}/{cover_image}\n")
                    index_file.write(":class-header: bg-light\n\n")

                    index_file.write(f"{card_title}\n\n^^^\ninsert summary here\n\n")
                    index_file.write(":::\n")

root_dir = r"C:\Users\Jose\Github\grasshopper-open-access-test\book\Grasshopper_Rhino_course\Knowledge_base\Tutorials"
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

root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Lessons"

rename_files_and_folders(root_dir)

update_markdown_links(root_dir)

```

# Create youtube iframes from youtube links


```python

import os
import re

def replace_youtube_links(root_dir):
    # Regex pattern to match YouTube URLs, both standalone and in markdown links
    pattern = r'\[?(https?://(?:www\.)?(?:youtube\.com/watch\?v=|youtu\.be/)([A-Za-z0-9_-]{10}[A-Za-z0-9_-]{1}))\]?(\(\1\))?'
    
    for dirpath, _, filenames in os.walk(root_dir):
        # Check only markdown files
        for filename in [f for f in filenames if f.endswith(".md")]:
            file_path = os.path.join(dirpath, filename)
            with open(file_path, 'r+', encoding='utf-8') as f:
                content = f.read()

                # Find YouTube URLs and replace with iframe embed link
                content_new = re.sub(pattern, r'<iframe width="560" height="315" src="https://www.youtube.com/embed/\2" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>', content)

                # If content has changed, write it back to the file
                if content != content_new:
                    f.seek(0)
                    f.write(content_new)
                    f.truncate()

root_dir = r"C:\Users\Jose\Github\grasshopper-open-access-test\book\test"
replace_youtube_links(root_dir)

```

# Turn single linebreaks into double line breaks

```python
import os
import re

def is_inside_code_block(line, is_in_block):
    if re.match(r'^(```|~~~)', line.strip()):  # fenced code block
        is_in_block = not is_in_block
    elif not line.strip().startswith('    ') and not is_in_block:  # not indented code block
        is_in_block = False
    elif line.strip().startswith('    ') and not is_in_block:  # indented code block
        is_in_block = True
    return is_in_block

def is_inside_table(line, is_in_block):
    if re.match(r'^\|.*\|$', line.strip()):
        is_in_block = True
    elif line.strip() == "":
        is_in_block = False
    return is_in_block

def double_linebreaks(root_dir):
    for dirpath, _, filenames in os.walk(root_dir):
        for filename in filenames:
            if filename.endswith('.md'):
                filepath = os.path.join(dirpath, filename)
                with open(filepath, 'r') as md_file:
                    lines = md_file.readlines()

                new_lines = []
                is_in_code_block = False
                is_in_table_block = False
                prev_line_empty = False
                for line in lines:
                    is_in_code_block = is_inside_code_block(line, is_in_code_block)
                    is_in_table_block = is_inside_table(line, is_in_table_block)
                    if not is_in_code_block and not is_in_table_block:
                        if not prev_line_empty and line.strip() and new_lines:
                            new_lines.append('\n')
                        new_lines.append(line)
                    else:
                        new_lines.append(line)
                    prev_line_empty = line.strip() == ""

                with open(filepath, 'w') as md_file:
                    md_file.writelines(new_lines)
root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Lessons"
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

root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Lessons"

boldify_text(root_dir)
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

root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Lessons"
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

root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Lessons"
process_directory(root_dir)

```


# Fix headers depth (H1 to H2 and so on)

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

root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Lessons"
process_directory(root_dir)

```

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

root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Lessons"
author = 'Your Name'
date_edited = date.today().isoformat()
process_directory(root_dir, author, date_edited)

```


# Formatting Tags (Notion tags to Jupyter Book tags)

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

root_dir = "/Users/localadmin/GitHub/grasshopper-open-access-test/book/Grasshopper_Rhino_course/Lessons"
process_directory(root_dir)

```

