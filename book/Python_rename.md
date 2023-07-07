made with chatgpt
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

youtube iframes


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

