## YouTube Video Downloader Documentation

This is a Python program that provides a graphical user interface (GUI) for downloading YouTube videos. It uses the `tkinter` library for creating the GUI components and the `pytube` library for handling the YouTube video downloads.

### Prerequisites

To run this program, you need to have the following dependencies installed:

- `tkinter`: It is a standard Python library for creating GUI applications.
- `pytube`: It is a library for downloading YouTube videos.

You can install `pytube` using the following command:

```
pip install pytube
```

### Program Functionality

The program allows the user to perform the following tasks:

1. Change the background color of the application window at regular intervals.
2. Get details of a YouTube video by entering its URL.
3. Download a YouTube video by entering its URL and selecting a download directory.
4. Clear the output labels.

### Program Code

The program is divided into several functions and GUI components. Here's an overview of each part:

1. Importing Required Libraries:

```python
import tkinter as tk
import random
from pytube import YouTube
from tkinter import filedialog
```

- The `tkinter` library is imported and aliased as `tk` for creating GUI components.
- The `random` module is imported for randomly choosing background colors.
- The `YouTube` class from the `pytube` library is imported for handling YouTube video downloads.
- The `filedialog` module from `tkinter` is imported for selecting the download directory.

2. Defining Color Palette:

```python
colors = ['#F44336', '#E91E63', '#9C27B0', '#673AB7', '#3F51B5', '#2196F3', '#00BCD4', '#009688', '#4CAF50', '#FFC107', '#FF9800', '#795548']
```

- A list of colors is defined. These colors will be used to change the background color of the application window.

3. Changing Background Color:

```python
def change_background():
    color = random.choice(colors)
    root.configure(background=color)

    # update foreground color based on background color
    if color in ['#F44336', '#E91E63', '#9C27B0', '#673AB7', '#795548']:
        output_color = 'white'
    else:
        output_color = 'black'
    status_label.config(fg=output_color)
    filepath_label.config(fg=output_color)

    # set font size to 22
    output_font = ('Arial', 22)
    status_label.config(font=output_font)
    filepath_label.config(font=output_font)

    root.after(5000, change_background)
```

- The `change_background` function is responsible for changing the background color of the application window.
- It selects a random color from the `colors` list and configures the root window with the selected color.
- The foreground color of the output labels (`status_label` and `filepath_label`) is updated based on the background color.
- The font size of the output labels is set to 22.
- The function uses the `root.after` method to schedule itself to run after every 5000 milliseconds (5 seconds).

4. Getting Video Details:

```python
def get_video_details():
    url = entry.get()
    yt = YouTube(url)

    # set video details
    title_label.config(text='Title: ' + yt.title)
    author_label.config(text='Author: ' + yt.author)
    views_label.config(text='Views: ' + str(yt.views))
    length_label.config(text='Length: ' + str(yt.length) + ' seconds')
```

- The `get_video_details` function is executed when the "Get Video Details" button is clicked.
- It retrieves the YouTube video URL entered by the user from the `entry` widget.
- It creates a `YouTube` object using the provided URL.
- The function sets the video details (title, author, views, and length) in the respective labels (`title_label`, `author_label`, `views_label`, and `length_label`).

5. Downloading Video:

```python
def download_video():
    url = entry.get()
    yt = YouTube(url)

    # open file dialog box to select download directory
    download_dir = filedialog.askdirectory()
    if download_dir:
        stream = yt.streams.get_by_itag(22) # choose the format you want to download
        stream.download(download_dir)
        status_label.config(text='Download completed!', fg='green')
        filepath_label.config(text='File saved at: ' + download_dir, fg='green')

        # center the output screen
        w = root.winfo_screenwidth()
        h = root.winfo_screenheight()
        x = int(w/2 - root.winfo_width()/2)
        y = int(h/2 - root.winfo_height()/2)
        root.geometry("+{}+{}".format(x, y))
```

- The `download_video` function is executed when the "Download" button is clicked.
- It retrieves the YouTube video URL entered by the user from the `entry` widget.
- It creates a `YouTube` object using the provided URL.
- It opens a file dialog box to allow the user to select a download directory.
- If a directory is selected, it retrieves the video stream with the specified format (itag) and downloads the video to the selected directory.
- The function updates the `status_label` and `filepath_label` with appropriate messages and sets their foreground colors to green.
- It also centers the application window on the screen.

6. Clearing Output:

```python
def clear_output():
    status_label.config(text='', fg=output_color)
    filepath_label.config(text='', fg=output_color)
```

- The `clear_output` function is executed when the "Clear Output" button is clicked.
- It clears the text and sets the foreground color of `status_label` and `filepath_label` to the output color determined by the current background color.

7. Creating the GUI:

```python
root = tk.Tk()
root.title('YouTube Video Downloader')

output_color = 'red'

# ... GUI component definitions ...
```

- The `root` window is created using the `Tk` class from `tkinter`.
- The title of the application window is set to "YouTube Video Downloader".
- The `output_color` variable is initialized to `'red'`. This is the initial color for the output labels.

8. Creating GUI Components:

```python
# ... GUI component definitions ...

change_background() # start changing background color

root.mainloop()
```

- Various GUI components such as labels, entry widgets, and buttons are created using the `Label`, `Entry`, and `Button` classes from `tkinter`.
- The `change_background` function is called to start changing the background color of the application window.
- The `mainloop` method is called on the `root` window to start the GUI event loop.

- 
  <h2 id="contributing">Contributing</h2>
  <p>Contributions are welcome! If you find any issues or would like to suggest enhancements, please feel free to submit a pull request or open an issue.</p>

  <h2 id="license">License</h2>
  <p>This project is licensed under the <a href="LICENSE">MIT License</a>.</p>
</body>
</html>


### Running the Program

To run the program, execute the Python script containing the code. The GUI window will appear, allowing you to interact with the YouTube video downloader. You can enter a YouTube video URL, get its details, download the video, and clear the output labels as needed. The background color of the window will change automatically every 5 seconds.
