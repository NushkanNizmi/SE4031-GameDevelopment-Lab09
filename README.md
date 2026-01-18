 # 🧪 LAB 09 (2 Hours) — Final Integration: Exit Door + Reset + Full Demo


---

## Objective

Integrate all previously developed VR mechanics into a complete mini VR application where the player starts, completes the full objective sequence, and unlocks the exit door.  
This lab also introduces a reset system to restart the experience by resetting counters and re-enabling collectable objects.

---

## Learning Outcomes

By the end of this lab, students will be able to:

- Integrate multiple VR interaction systems into one complete application flow  
- Implement an exit condition based on objective completion  
- Control scene progression by enabling/disabling key gameplay objects  
- Implement a reset system that restores game state and interactable objects  
- Reset and refresh UI counters through the GameManager  
- Validate a full end-to-end VR experience through a final demo  
- Troubleshoot XR Interaction Toolkit component differences across templates  

---

## Goal

Create a mini VR application:

start → objectives → exit opens.

---

## A) Exit Door

Create Cube → rename **ExitDoor** (block path)

Create empty object **ExitController**

Create script **ExitController.cs**:

```csharp
using UnityEngine;

public class ExitController : MonoBehaviour
{
    public GameObject exitDoor;

    void Update()
    {
        if (ObjectiveManager.Instance && ObjectiveManager.Instance.Completed())
            exitDoor.SetActive(false);
    }
}
```
Attach to ExitController
Drag ExitDoor into `exitDoor`

---

## B) Reset System (Keyboard R)

Create empty object **ResetManager**

Create script:

```csharp
using UnityEngine;

public class ResetManager : MonoBehaviour
{
    public GameObject[] collectables;

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.R))
        {
            if (GameManager.Instance)
            {
                GameManager.Instance.gems = 0;
                GameManager.Instance.keys = 0;
                GameManager.Instance.targetsHit = 0;
                GameManager.Instance.RefreshUI();
            }

            foreach (var c in collectables)
                if (c) c.SetActive(true);

            if (ObjectiveManager.Instance)
                ObjectiveManager.Instance.UpdateObjective();
        }
    }
}
```
In Inspector: drag all placed gem/key objects into `collectables[]`

---

## Final Submission (2–3 min video)

Must show:

- locomotion  
- collecting gems/keys  
- hit targets  
- lore popup  
- objective completion  
- exit door opens  
- press **R** resets counters + items reappear  

Filename: Lab09_Final_<ITNo>.mp4


⚠️ **Important Note**

Students must submit **all project files to GitHub** along with the demo video.

Both of the following are mandatory:

- Complete Unity project pushed to a GitHub repository  
- Demo video file uploaded or shared with the submission  

Submissions without the GitHub project files will be considered incomplete.

---

