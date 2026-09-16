
This repository is meant to act as a visual snapshot of the python development I have been contacted to do for the subject 48024 Programming 2 at UTS.
As this content is UTS IP, only small snippets can be shown.

<details>
<summary><strong>Assignment Development</strong></summary>

<br>
Programming 2 is one of very few subjects that are permitted to develop a brand new major assignment each semester. Although there are general guidelines to follow regarding difficulty, scope, expected data structures and restrictions, it is my job to fully design, develop and maintain the entire assessment through it's 2 major components:

- Assignment 1
    - 35% of the grade
    - Developed as a console application in **Java** OR **Python**
- **Assignment 2**
    - 25% of the grade
    - Developed as a GUI application in **JavaFX** OR **Tkinter**

The same case study is shared across both assignments.

## Assignment 1

Both assignments are heavily focused on understanding and implementing object-oriented principles. Designing the class strucuture of the assignment is a delicate balance between ensuring students are challenged and presented with good principles, whilst also being at a difficulty level that is feasible for them to achieve within the timeframe.

![class_diagram](/image/assignment/class_diagram.png)
_**Example**_: The class diagram from Autumn 2026 which models an imaginary card game named 'Around the Table'

Students are given the class diagram, specification, and starting scaffold. This means I need to balance which classes/functions students are given and which are expected to be developed.

Although rare, this sometimes gives me the opportunity to provide something more intermediate/advanced as part of the scaffold to encourage them to learn something new without an unncessary challenge.

```python
class League:
    _instance = None
    def __init__(self, seeded_teams, seeded_players, seeded_managers):
        self.teams = seeded_teams
        self.manageable_teams = Teams([team for team in self.teams.get_teams() if team.get_manager() is None])
        self.players = seeded_players
        self.managers = seeded_managers
        self.logged_in_manager = None

    @staticmethod
    def initialize(seeded_teams, seeded_players, seeded_managers):
        if League._instance is None:
            League._instance = League(seeded_teams, seeded_players, seeded_managers)

    @staticmethod
    def get_instance():
        if League._instance is None:
            pass
        return League._instance

league = League(seeded_data.get_teams(), seeded_data.get_players(), seeded_data.get_managers())
```
_**Example**_: The singleton pattern implemented for the League class in the spring 2025 assignment

Student's also need to be presented with a working solution. For every assignment, a clean implementation that matches 1-to-1 with their expected output is developed by myself and integrated into EdStem using Edstem's 'Check' feature.

![check_code](/gif/check.gif)

## Assignment 2

Assignment 2 involves recreating Assignment 1 as a GUI. I refactor the solution code from Assignment 1 such that:
- Input/output are removed (since these will both come from UI interactions)
- Errors are changed from print statements to instead throw custom exceptions out of the function

```python
def __place_main(self, main):
    self.__view()
    if self.__hand_full():
        print(f"Hand is full. Main card played automatically!")
        return main
    choice = input("Would you like to place main in your hand (h) or play (p): ")
    if choice == 'p':
        return main
    else:
        self.__hand.append(main)
    return None
```
```python
def place(self, card):
    if self.hand_full():
        raise FullHandException("Hand is full!")
    self.__temp_hand.remove(card)
    self.__hand.append(card)
    self.calculate_health()
```

Once again, a clean 1-to-1 solution is developed by myself for use in a video demonstration that showcases how each window is expected to look and behave, and which windows should open from which interaction.

Some aspects of GUI development in Tkinter are extremely tedious, such as creating `Image` widgets. Students are provided with a `TkUtils` class, developed by myself, which contains helper classes and functions to ease development.

```python
class TkUtils:
    #...
    class Image(tk.Label):
        def __init__(self, parent, path, width, height, background=None):
            image_ = PIL.ImageTk.PhotoImage(PIL.Image.open(path).resize((width, height)))
            super().__init__(parent, image=image_, background=background)
            self.photo = image_
```

The visual design and layout of the GUI is designed by myself. This is a balance between creating something that is aesthetically pleasing, whilst still being simple enough for students to recreate without complex widgets that aren't covered in the subject material.

From 2026 Autumn onwards, the visual assets have also been created by myself.

![showcase](/image/assignment/gui_showcase.png)

</details>

<details>
<summary><strong>Refresher Content</strong></summary>

<br>
Programming 2 includes a "Week 0" module with various introductory ativites. "Refresher" activities are included for both Java and Python. Although slides existed for Python already, there were no dedicated coding challenges. I was permitted to add various coding challenges to improve the student's understanding of fundamental python syntax and logic.

## Slides
The existing text-based slides for python were fantastic and I only felt the need to add 1 extra slide, dedicated to slicing.

![Slicing](/image/refresher/slicing.png)

## Code Challenges
Some challenges were presented "as is". That is, there were no requirements to actually complete the code and were merely to showcase a feature that students may need to be _aware_ of, but not necessarily need to know how to implement

![class_as_is](/image/refresher/refresher_1.png)
_**Example**: A Movie class_


Some challenges required students to "fill in the gaps" to complete the specificaton.

![operator](/image/refresher/refresher_2.png)
_**Example**_: An exercise to practice using the modulo and integer division operator


The final challenge was presented more as a "walkthrough" to complete an object oriented program, which was highly relevant to the content that would be presented in the subject

![walkthrough](/image/refresher/refresher_3.png)
_Movie program walkthrough_

</details>

<details>
<summary><strong>GUI Development</strong></summary>

<br>
As part of the transition from a Java-only subject to a Java-Python hybrid subject, a large amount of Python content needed to be created to match the existing Java content.

As of 2026, some study module content relating to Tkinter GUI was still needed. Although some videos did exist, I used this as an opporunity to fully overhaul all aspects of the Tkinter content for the subject to include best practices and keep approaches consistent across all aspects of the subject.

To do this, I developed:
- High quality slides for modules 7, 8, 9 and 10,
- Code demos to accompany the concepts shown in the slides,
- Scripted 1-hour long "lecture-style" video recordings to present the slides and accompanying code, and
- Reworded weekly labs for weeks 8, 9, 10 and 11 to match the approaches taught in the video recordings 

An example for each is presented below:

## Slides
![slides](/image/tkinter/slide.png)
_**Example**_: A tkinter slide from Study Module 8

## Demo code
![studymodule](/image/tkinter/code.png)
_**Example**_: A code demo from Study Module 10

## Lecture recording
<video src="https://github.com/user-attachments/assets/acb33814-76fe-46a5-9ce5-c941554b14f2"></video>
_**Example**_: A short clip from Study Module 9

## Lab task
![lab](/image/tkinter/lab_comparison.png)
_**Example**_: A snippet of the instructions from Lab 10 compared to the old, unclear instructions

In creating this content, I had an unusual responsibility of trying to balance demonstrating best practices for Tkinter, **whilst still trying to keep the approach as close as possible to our Java counterpart**. This is a quirk of the subject that is not in my control.

For this, 2 innovative approaches that were developed by myself from scratch were:
- Dictionary destructuring to create "css-style" stylesheets for widgets, and
- An adaption of the MVC pattern, combined with the observer pattern, to create GUIs to display model data and react to changes in model state

```python
class Style:
    button = {
        "font": ("Monospace", 16, "bold"),
        "background": "red",
        "foreground": "white"
    }
    padding_small = {
        "pady": 10
    }
```
```python
#...
ttk.Separator(self.parent, orient=HORIZONTAL).grid(row=2, column=0, columnspan=2, sticky=EW, **Style.padding_small)

Button(self.parent, **Style.button, text="Open", command=self.open).grid(row=3, column=0, sticky=EW)
Button(self.parent, **Style.button, text="Record Win", command=self.win).grid(row=3, column=1, sticky=EW)
```
_**Example**_: A widget styled using dictionary destructuring

```python
class Team:
    def __init__(self, local_name, team_name, wins, losses):
        self.__local_name = local_name
        self.__team_name = team_name
        self.__wins = wins
        self.__losses = losses
        
        self.subscribers = []
        
    def subscribe(self, subscriber):
        self.subscribers.append(subscriber)
    
    def unsubscribe(self, subscriber):
        self.subscribers.remove(subscriber)
    
    def notify(self):
        for subscriber in self.subscribers:
            subscriber.handle()
    
    def add_win(self):
        self.__wins += 1
        self.notify()
```
```python
class TeamView:
    def __init__(self, parent, model: Team):
        self.parent = parent
        self.model = model
        
        self.model.subscribe(self.update_percent_label)
        
        #...

        Button(self.parent, text="Close", command=self.close).grid(row=5, column=0)

    def close(self):
        self.model.unsubscribe(self.update_percent_label)
        self.parent.destroy()

    def update_percent_label(self):
        self.percent_lbl.configure(text=self.model.get_win_percent())
```
_**Example**_: A window using the MV/Observer design pattern

</details>