# Setup
import google.generativeai as genai
genai.configure(api_key='#Insert API key from https://ai.google.dev/gemini-api/docs/api-key')
from tkinter import *
window = Tk()
from gtts import gTTS
import pygame

# Variables and functions
number_of_words = IntVar()
text_to_summarize = ""


def summarize_text():
    global number_of_words, text_to_summarize, response2
    num_words = number_of_words.get()
    text_to_summarize = text_input.get("1.0", "end-1c")
    model = genai.GenerativeModel('gemini-pro')
    response = model.generate_content(f'Summarize the following text: {text_to_summarize}. Do this summary in exactly {num_words} words')
    response2 = response.text
    summary_box.config(wrap='word')
    summary_box.insert(END, response2)

def read_aloud():
    global response2
    language = 'en'
    myobj = gTTS(text=response2, lang=language, slow=False)
    myobj.save("text_summary.mp3")
    pygame.mixer.init()
    pygame.mixer.music.load("text_summary.mp3")
    pygame.mixer.music.play()
    
# Components
title_label = Label(window, text="Text summarizer", pady=10)
title_label.config(font=("Arial", 20))
title_label.pack()

text_label = Label(window, text="Text to summarize")
text_label.pack()

text_input = Text(window, height=15, width=45)
text_input.pack()

slider_label = Label(window, text="Number of words in summary", padx=100)
slider_label.pack()

slider = Scale(window, variable=number_of_words, from_=1, to=250, orient=HORIZONTAL)
slider.pack()

blank_label = Label(window, text="\n")
blank_label.config(font=("Arial", 7))
blank_label.pack()

run_button = Button(window, text="Summarize", command=summarize_text)
run_button.pack()

scrollbar = Scrollbar(window)
scrollbar.pack(side=RIGHT, fill=Y)

summary_box = Text(window, width=50, height=10, yscrollcommand=scrollbar.set)
summary_box.pack(fill=BOTH, expand=1)

read_aloud = Button(window, text="Read aloud", command = read_aloud)
read_aloud.pack()

scrollbar.config(command=summary_box.yview)

label1 = Label(window, text="Summaries powered by gemini API")
label1.config(font=("Arial", 10))
label1.pack()

window.mainloop()
