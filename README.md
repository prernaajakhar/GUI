import tkinter as tk
from tkinter import messagebox

def fetch_lyrics():
    song = song_entry.get()
    artist = artist_entry.get()
    if not song or not artist:
        messagebox.showwarning("Input Error", "Please enter both song title and artist name.")
        return
    
    try:
        # Fetching lyrics
        lyrics = genius.search_song(song, artist).lyrics
        lyrics_text.delete(1.0, tk.END)
        lyrics_text.insert(tk.END, lyrics)
    except Exception as e:
        messagebox.showerror("Error", f"Could not fetch lyrics: {str(e)}")

# Setting up the GUI window
root = tk.Tk()
root.title("Lyrics Extractor")

# Song title label and entry
song_label = tk.Label(root, text="Song Title:")
song_label.pack()
song_entry = tk.Entry(root, width=50)
song_entry.pack()

# Artist name label and entry
artist_label = tk.Label(root, text="Artist Name:")
artist_label.pack()
artist_entry = tk.Entry(root, width=50)
artist_entry.pack()

# Search button
search_button = tk.Button(root, text="Search", command=fetch_lyrics)
search_button.pack()

# Text box to display lyrics
lyrics_text = tk.Text(root, wrap=tk.WORD, width=60, height=20)
lyrics_text.pack()

root.mainloop()
