---
layout: post
title:  "Typist for 10FastFingers"
date:   2019-05-26 14:42:00 -0500
categories:
---

About a month ago, a friend approached me and asked if I could make a typing bot since it could be similar to my [ManiaBot](https://nguyenjus.github.io/blog/ManiaBot/). I immediately figured I would need to train the AI on the font to detect the letters that it needed to type. Since I was not confident in machine learning and the project was on a time-constraint, I declined. Two days later, I found Google's Tesseract OCR, sparking my journey into creating a new AI.

![gif](https://media.giphy.com/media/JRJv30eoBRF1Sb9tcO/giphy.gif)

Although the gif is bad quality, you can see how fast (can go faster!) and how correctly (green words!) the AI is typing!





## **Introduction**
We want to write a bot that can read the letters on the screen and type them, preferably like a human with delays between the keystrokes. Why 10fastfingers? Well because I didn't have access to my friend's site and 10fastfingers seemed like the simplest cascading-text-lines typing test on the first page of Google's search.

We can read the screen using PIL. We can find letters using Tesseract OCR. We can type using pynput. So we can combine all of the above to make a typing test bot! Great! Simple.

## **Reading Text**
In order to read the text, we must read the screen first. To do this, I used PIL:

```
im = ImageGrab.grab(bbox=92,244,934,340))
```

This grabs the image box containing only the words that we need to type.

Now, here's where I originally got stuck. Believe me if you want, but I dreamed of a module that came pre-trained on various characters. Lo and behold, when I searched it up, I found [exactly what I needed](https://youtu.be/jWh0FaRRZC4)!

```
text = pytesseract.image_to_string(im, lang = 'eng')
```

This is amazing because it will help with the French, Spanish, Portuguese, and the other language modules too! Now, we can print to test what kind of words the AI thinks is on the screen.

![img](http://i.imgur.com/roEGDOp.png)

## **Typing Text**
If you had read about my ManiaBot, this part is easy with pynput. However, I decided to play with [Keyboard](https://github.com/boppreh/keyboard) instead.

```
for letter in lines:
    if kill() or not check_window():
        return
    elif letter == '\n':
        keyboard.press_and_release('space')
    elif letter.isupper():
        keyboard.press_and_release('shift +' + letter)
    else:
        keyboard.press_and_release(letter)
        time.sleep(random.uniform(11/wpm,13/wpm))
keyboard.press_and_release('space')
```

Each time we type, we must check if the conditions are still good (user hasn't killed the program and is in the appropriate window). This is what kill() and check_window() functions are for. Line breaks are considered spaces, so we check for that too. At the end of the text, we should also space to move onto the new lines. Keyboard has this small issue where it types the letter in lowercase even if it is uppercase, so we deal with that by holding shift when necessary.

I added random delays after pressing each letter for ~~cheating~~ legacy purposes. The delay per wpm does not calculate perfectly for a few reasons. First, PIL and Tesseract take a small amount time to process data. Secondly, I had to add a small delay between typing and next image capture since there may be delays updating the typing text on the website. Lastly, f(x) = C/x is an asymptotic function so it will not scale linearly with a linear increase in WPM. The best ranges to use the test are 40-150 WPM. Higher than that, the user needs to increase the 'WPM' parameter further to actually reach the WPM they desire.

## **Kill Switch**
We're basically done, but we just need some way to kill the AI in case it attempts to take over the computer. I added a few countermeasures to combat this issue. I wrote these in the form of flags to check at each phase of the program. First, the user needs to be in the correct window. That is, the browser window containing the typing test. Have you ever tried to type while in a different window? No, it does not work. win32ui works only on Windows (sorry Mac users).

```
def check_window():
    return '10FastFingers.com' in win32gui.GetWindowText(win32gui.GetForegroundWindow())
```

The loop runs while the window title contains "10FastFingers.com", which can backfire if other windows have the phrase in their window names too, but what's the likelihood of that... If this is the case, a more specific condition may be used.

Secondly, the AI checks for text repetition. If the new text is the exact same as the old text, chances are that the lines did not cascade (change) and the test is complete or an error arose. This may backfire if two consecutive texts are intentionally the same.

```
def flag(oldtext, newtext):
    return oldtext == newtext
```

Just a simple flag function which compares the saved old text with the current new text.

Finally, a dedicated kill switch! It took me a little bit of time and switching to the new keyboard module to get this to work. Basically, another flag is raised if the program detects ESC button is clicked. There's a bit of latency issue, so the user should hold ESC for less than half a second instead of tapping it.

```
def kill():
    return keyboard.is_pressed('esc')
```

Just a simple flag function that detects if ESC is clicked.

With these three flags, I'm fairly confident that the user has most control over the program. Earlier renditions of this program resulted in AI takeover, where the AI would continue typing no matter what, resulting in creation of new files, windows, etc.

## **Config**
I decided to write a config script to help configure the AI for any screen/window size and typing speed! This came to mind when I wanted to dynamically change the bounding box of PIL image capture. Here's what I did:

```
...
print('Now hover your mouse over the TOP-LEFT corner of your desired text box.')
input('Press enter when complete (do not move or click mouse)')
topleft = win32gui.GetCursorPos()
config['leftx'] = topleft[0]
config['topy'] = topleft[1]
...
```

This is just a walkthrough script. First, the user should place their mouse cursor in the top left corner of the text box. The cursor position is calculated by win32gui immediately after the user presses "Enter." The same can be done for the bottom right corner of the text box. As a result, we can generate a box where PIL and Tesseract should capture text from. In this script, the WPM can be specified as well. All of this is saved into a json file and read back by the actual typing AI. Minimal, but I thought I did a cool job!

## **Code**
You can find it [here on my Github](https://github.com/NguyenJus/Typist-for-10fastfingers).

## **Wrap Up**
Initially, I thought I would have to train the AI for character recognition, but it turns out someone else (Google) had already done it for me. This essentially turned my problem into a ManiaBot template. Really, both bots are doing the same thing, just in different ways! It's cool to be able to reuse what I've learned in past works.

I am currently learning [Machine Learning](https://www.coursera.org/learn/machine-learning/home/welcome), so hopefully soon I can bring more advanced projects to the table.

## **Videos**

From fast to slow, I have four videos. Notice in the fastest one, 10FastFingers does not even have a condition to check if the typing test is complete before one minute is up!

<iframe width="560" height="315" src="https://www.youtube.com/embed/Rdn4HolKUmI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Here's an impossibly fast, *but not too fast* test.

<iframe width="560" height="315" src="https://www.youtube.com/embed/J4oCThX3hCM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Just your average 100 WPM tester below.

<iframe width="560" height="315" src="https://www.youtube.com/embed/fhJw9IXGLuM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Last but least, 45 WPM.

<iframe width="560" height="315" src="https://www.youtube.com/embed/HtuTsCHvL6g" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
