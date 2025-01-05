# Import tools that you need
  import os
  from PIL import Image

# Define the WEBP file and JPG file and check the folder that exist
  def convert_webp_to_jpg(source_folder, target_folder):

    # Checking the folder
    if not os.path.isdir(source_folder):
        print(f"Folder source '{source_folder}' not found.")
        return

    # Make the new target folder
    os.makedirs(target_folder, exist_ok=True)

    # Iteration
    for filename in os.listdir(source_folder):
        if filename.lower().endswith('.webp'):
            webp_path = os.path.join(source_folder, filename)
            jpg_path = os.path.join(target_folder, os.path.splitext(filename)[0] + '.jpg')

            try:
                # Open WEBP file and convert it to JPG
                with Image.open(webp_path) as img:
                    img = img.convert('RGB')  # Convert to RGB format
                    img.save(jpg_path, 'JPEG')
                print(f"Convert Successed: {filename} -> {os.path.basename(jpg_path)}")
            except Exception as e:
                print(f"Convert Failed {filename}: {e}")

    print("Convert Process Finished.")

# Example for your source folder and target folder
source_folder = r"GRISAIA"
target_folder = r"GRISAIA JPG OMA"
convert_webp_to_jpg(source_folder, target_folder)
