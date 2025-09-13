import os
import requests
from urllib.parse import urlparse

def fetch_image(url):
    try:
        # Send a GET request to the URL
        response = requests.get(url)
        
        # Check if the request was successful
        response.raise_for_status()  # Raises an HTTPError for bad responses
        
        # Create directory if it doesn't exist
        os.makedirs("Fetched_Images", exist_ok=True)
        
        # Extract filename from URL or generate one
        parsed_url = urlparse(url)
        filename = os.path.basename(parsed_url.path) or "downloaded_image"
        
        # If filename doesn't have an extension, add one
        if not filename.lower().endswith(('.png', '.jpg', '.jpeg', '.gif')):
            filename += '.jpg'  # Default to .jpg
        
        # Save the image in binary mode
        with open(os.path.join("Fetched_Images", filename), 'wb') as f:
            f.write(response.content)

        print(f"Image successfully downloaded and saved as: {filename}")

    except requests.exceptions.HTTPError as http_err:
        print(f"HTTP error occurred: {http_err}")
    except requests.exceptions.RequestException as req_err:
        print(f"Request error occurred: {req_err}")
    except Exception as e:
        print(f"An error occurred: {e}")

if __name__ == "__main__":
    image_url = input("Please enter the image URL: ")
    fetch_image(image_url)
