# Unity-code
Here’s a basic Unity C# script to open a door when the player interacts with it. This script assumes that the door is a GameObject that rotates around its Y-axis when opened.
using UnityEngine;
public class DoorController : MonoBehaviour
{
   public float openAngle = 90f; // How far the door will open
   public float closeAngle = 0f; // The original angle when closed
   public float smooth = 2f; // Speed of the door opening
   public bool isOpen = false; // Is the door currently open
   private Quaternion targetRotation;
   void Update()
   {
// Rotate the door towards the target angle (open or close)
       transform.localRotation = Quaternion.Slerp(transform.localRotation, targetRotation, Time.deltaTime * smooth);
   }
   public void ToggleDoor()
   {
// Toggle between open and closed states
       if (isOpen)
       {
           targetRotation = Quaternion.Euler(0f, closeAngle, 0f);
       }
       else
       {
           targetRotation = Quaternion.Euler(0f, openAngle, 0f);
       }
       isOpen = !isOpen;
   }
   private void OnTriggerEnter(Collider other)
   {
// If the player enters the trigger zone, toggle the door
       if (other.CompareTag("Player"))
       {
           ToggleDoor();
       }
   }
}
How it works:
1. Attach this script to the door GameObject in your scene.
2. Make sure the door has a collider set as a trigger and that the player has a tag of “Player.”
3. The door will rotate around its Y-axis when the player enters the trigger zone. The ToggleDoor method opens or closes the door by adjusting its rotation.
You can tweak openAngle, smooth, and other parameters to fit your specific game.
