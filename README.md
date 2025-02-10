# What

This Jupyter Lab showcases multi-modal capabilities of OpenAI. There are two parts:

1. Text based crowd analysis
2. Image and voice based crowd analysis

To get started, you'll need to configure your api key

## Configuration

This homework assumes you figured out how to create your open ai API key. Once you have the key, open the `.env` file inside the root directory. You can do this on macOS with `open .env -a TextEdit`.

Replace <Your key here> with your API key.

## Testing Part 1

Open the Jupyter lab using the `jupyter lab` command. Run through the code blocks until you hit the first GUI. You should be prompted to add an image url. 

Go to Google images, and search for "a few people" and look for some images. Once you find one to your liking, get the image address via the following steps:

1. Click into it and reveal the slightly enlarge thumbnail
2. Right click the enlarged image and click "Copy Image Address"

With your image url, go back to the Jupyter lab and paste the image url. Hit submit and wait for the crowd detection app to return you a result.

This app specifies that a result with more than 10 people will trigger a warning. 

## Testing Part 2

The second part of the lab takes two inputs - an image url and a voice clip. It then returns a voice representation of the crowd size from the image, and a picture representing the situation.

Run through the code blocks until you find the next GUI. Find an image url like the first part, and then record a voice clip asking the amount of people in the picture.

You should receive a voice clip telling you how many people there are, and an image representing the situation.