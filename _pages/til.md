---
title: "TIL"
permalink: /til/
author_profile: false
---
# DEPRECATED , TIL ARE NOW SEPARATE POST EACH DAY

## 19th January 2020
- To set a keyboard shortcut to a script in ubuntu, save the script with chmod +x in some place thats included in PATH (usually ~/bin/) and add this to the keyboard shortcut command field:
	```
	gnome-terminal -e <script.sh>
	```
- introduction to RNN, basic neural net with some sort of memory or consideration of a series of inputs. some idea of finite response models (partially recurrent) and state space models and the idea of back propagation through time.
- recall/precision as error metrics for skewed classes and using them together as F score.
- a little bit of geometric interpretation of vectors in context of applied multivariate statistics.
- little bit of beautifulsoup4, its an easy way to parse entire html pages that you get with requests in python.

	```python
	soup = bs4(url, "html.parser")
	soup.find("a") => returns a tag
	```

    
## 18th January 2020
- I have no clue how to implement conv1d... wtf is out_width / in_width and why are they not equal???? it makes sense for out channels to be different from in channels but wtf is up with widths?? isnt conv1d just supposed to sweep over the entire width???
<img src="https://i.imgur.com/P18Mc2B.gif" alt="image showing conv1d" width="500" height="500">

- Can embed images in github like this 
  ```html
    <img src="https://i.imgur.com/P18Mc2B.gif" alt="image showing conv1d" width="500" height="500"/>

    ![](https://i.imgur.com/P18Mc2B.gif)
  ```
- Can make gif animations by making each frame with inkscape then combining..
- Apparently plank was no revolutionary, he was a [data fitterer](https://physicsworld.com/a/max-planck-the-reluctant-revolutionary) 
- Also learned how to install plugins in vim using vim-plug (just put "Plug 'name of plugin'" into the .vimrc file and done. 
- setup a markdown preview thing for vim so I can write to this file directly from the terminal.
- install from .deb file in ubuntu:
	```
	sudo dpkg -i /path/to/deb/file
	sudo apt-get install -f
	```

## 17th January 2020
- spaCy has a pretty good displacy thing for viewing syntactic dependencies
- How to install node on ubuntu (curl that bash thing) the bad way.
- React is a webdev thing (_npx create-react-app_)
- just edit the --- thing at top of md file to change [jekyll properties instead of config.yml](https://jekyllrb.com/docs/configuration/front-matter-defaults/)
