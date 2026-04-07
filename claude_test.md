# Comprehensive Summary: ProgramADAS Unity Game Project

## Project Overview

ProgramADAS is an educational game developed by students at UFJF (Universidade Federal de Juiz de Fora) to promote programming education and gender equality in computer science.  
The game uses Unity 2022+ with a 2D top-down perspective, featuring a narrative-driven gameplay with multiple mini-games and educational content.

---

## 1. Overall Project Structure


/home/lucas/Downloads/ProgramADAS/
├── Assets/
│ ├── Animations/ (Character and UI animations)
│ ├── Cutscenes/ (Timeline cutscene assets)
│ ├── Fonts/ (Custom fonts for UI)
│ ├── Prefabs/ (Reusable game objects)
│ ├── Scenes/
│ │ ├── Menus/ (Menu scenes)
│ │ ├── Rooms/ (Game room scenes)
│ │ └── Cutscenes/ (Cutscene scenes)
│ ├── Scripts/ (Core game logic - 69 C# files)
│ └── TextMesh Pro/ (Third-party text rendering)
├── Packages/ (Unity package dependencies)
├── ProjectSettings/ (Build configurations)
├── Library/ (Build cache)
└── README.md (Developer guide in Portuguese)


### Key Technologies

- Unity 2022 LTS  
- C# scripting  
- TextMesh Pro (UI text rendering)  
- 2D Physics (Rigidbody2D)  
- Scene Management  
- Serialization / Save System  

---

## 2. Key Architecture Patterns

### Singleton Pattern for Managers

Multiple managers use the singleton pattern for global access:

- GameManager — Core game state and progress tracking  
- DataPersistenceManager — Save/load system  
- DialogueManager — Dialogue UI display  
- NotepadManager — Educational content system  
- QuestManager — Quest objectives display  
- SoundManager — Audio playback  
- TransitionManager — Scene transitions  
- SpawnManager — Player spawn positions  
- CafeManager — Minigame Café state  
- Fase3Manager — Minigame Billiards state  

---

### Interface-Based Data Persistence

`IDataPersistence` interface ensures all game systems can participate in save/load:

```csharp
public interface IDataPersistence {
    void LoadData(GameData data);
    void SaveData(ref GameData data);
}
3. Script Organization & Purposes
Core Managers (/Assets/Scripts/Managers/)
Script	Purpose
GameManager.cs	Tracks game progress, quiz scores, unlocked chapters, and manages exclamation markers for NPCs
DataPersistenceManager.cs	Handles all game save/load via JSON with optional encryption; triggers on scene loads
FileDataHandler.cs	Low-level file I/O for serialized game data using XOR encryption with "ProgramADA" key
QuestManager.cs	Displays dynamic quest objectives based on game progress (8 progression states)
TransitionManager.cs	Manages scene transitions with fade-in/fade-out animations
SpawnManager.cs	Stores player respawn positions per room
SoundManager.cs	Singleton for playing UI sound effects (correct, wrong, click, cancel)
MusicManager.cs	Manages background music (referenced but not heavily developed)
MouseManager.cs	Handles mouse input interactions
Player System (/Assets/Scripts/Player/)
Script	Purpose
PlayerMovement.cs	2D character controller with WASD/arrows movement and Left Shift sprint (6x speed)
PlayerData.cs	Saves/loads player position and calculates game completion percentage
OrderingSprites.cs	Manages player sprite layering for proper depth sorting
Dialogue & Story (/Assets/Scripts/Dialogue/)
Script	Purpose
Dialogue.cs	Data structure for dialogue lines with character images and text
DialogueManager.cs	Displays dialogue with typewriter effect, handles line progression
DialogueTrigger.cs	Activates dialogue when player presses 'E' near NPCs; shows tooltip
Quiz System (/Assets/Scripts/Quiz/)
Script	Purpose
QuizManager.cs	Manages quiz questions, scoring (pass = 75%), and unlocks Chapter 2 on success
QuizAnswerScript.cs	Individual answer button logic
QuizTrigger.cs	Initiates quiz when player interacts with specific NPCs
QuestionAndAnswers.cs	Data structure for quiz questions and multiple choice answers
Mini-Game: Café (/Assets/Scripts/MiniGame/)
Script	Purpose
CafeManager.cs	Main café minigame controller; saves score to pointFases[1]
StartMiniGameManager.cs	Dialog box asking player if they want to start minigame
Orders.cs / Order.cs	Manages customer orders and order queue
Clients.cs	Customer/NPC data and sprites
Foods.cs / Drinks.cs	Available food/drink items player can select
ButtonsMiniGame.cs	UI button handling for minigame interaction
ScoreCafe.cs	Scoring system (starts at 100%, loses 8–16% per error); shows win/lose screen
FeedbackManager.cs	Displays error feedback with NPC images and explanatory text
Feedback.cs	Data structure for feedback messages
FeedbackTrigger.cs	Triggers specific feedback based on player errors
Mini-Game: Billiards (Fase3) (/Assets/Scripts/Fase3/)
Script	Purpose
Fase3Manager.cs	Main billiards game controller; saves score to pointFases[2]
StartFase3.cs	Initiates fase 3 gameplay
Bola.cs	Ball physics and interaction logic
Condicao.cs	Win/lose condition checking