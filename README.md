# Text-to-speech-mystic
from gtts import gTTS 
import os
import ipywidgets as widgets

from IPython.display import display,Audio

LANGUAGES = {
"English":"en",
"malayalam":"ml",
"Hindi":"hi",
"tamil":"ta"
}


#FunctiontoConvertTexttoSpeech

def text_to_speech(text,lang="en",slow=False): 
    try:
      tts=gTTS(text=text,lang=lang,slow=slow) 
      tts.save("output.mp3")
      return Audio("output.mp3",autoplay=True) 
    except Exception as e:
      print(f"Error:{e}")

def tts_interface():
    print("Welcome to the Text-to-Speech System!!")

#TextInputBox
text_input=widgets.Textarea(
placeholder="Enter the text you want to convert to speech...", layout=widgets.Layout(width="100%", height="100px")
)

lang_dropdown=widgets.Dropdown(
options=LANGUAGES.keys(), value="English", description="Language:",
style={'description_width':'initial'}
)
#SpeedToggle

speed_toggle=widgets.Checkbox( value=False,
description="SlowMode"

)

generate_button=widgets.Button(
description="ConverttoSpeech", button_style="success"
)

#DisplayWidgets

display(text_input,lang_dropdown,speed_toggle,generate_button)

# Button Click Event
def on_button_click(b):
    text = text_input.value.strip()  # get the text input
    language = LANGUAGES[lang_dropdown.value]
    slow_mode = speed_toggle.value

    if text:  # Correct condition
        print("\nPlaying Speech...")
        display(text_to_speech(text, lang=language, slow=slow_mode))  # Use 'text'
    else:
        print("Please enter text to convert!")

generate_button.on_click(on_button_click)

#RuntheInterface 
tts_interface()