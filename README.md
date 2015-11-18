using UnityEngine;
using UnityEngine.UI;
using System.Collections;

public class TextController : MonoBehaviour {

    public Text text;
    private enum States { cell, mirror, sheets_0, lock_0, cell_mirror, sheets_1, lock_1, freedom };
    private States myState;
    void Start() {
        myState = States.cell;
    }

    // Update is called once per frame
    void Update() {
        if (myState == States.cell){state_cell();
        } else if (myState == States.sheets_0) {state_sheets_0();
        } else if (myState == States.lock_0){state_lock_0();
        } else if (myState == States.mirror) {state_mirror();
        } else if (myState == States.cell_mirror) { state_cell_mirror();
        } else if (myState == States.sheets_1) { state_sheets_1();
        } else if (myState == States.lock_1) { state_lock_1();
        } else if (myState == States.freedom) { state_freedom();  }

    }
    void state_cell()
    {
        text.text = "You are locked in a prison cell. You want to escape. " +
                   "There is a mirror on the wall of the cell, dirty sheets on your " +
                   "bed and you realize that the door is locked from the outside.\n\n" +
                   "Press M to examine the Mirror, S to examine the Sheets, and L to examine Lock";
        if (Input.GetKeyDown(KeyCode.S)){myState = States.sheets_0;}
        if (Input.GetKeyDown(KeyCode.M)) { myState = States.mirror; }
        if (Input.GetKeyDown(KeyCode.L)) { myState = States.lock_0; }
    }
    void state_sheets_0()
    {
        text.text = "Even for a prison these sheets are filthy! " +
            "After some quick examination of the stain splatter rags you decide they " +
            "are useless.\n\n" +
            "Press R to Return to exploring your cell";
        if (Input.GetKeyDown(KeyCode.R))
        {
            myState = States.cell;
        }
    }
    void state_lock_0()
    {
        text.text = "The lock appears to one of those pass code locks. " +
          "You feel as though you might be able to see where the dirty finger prints were " +
          "if you could see the front of the lock.\n\n" +
           "Press R to Return to exploring your cell";
        if (Input.GetKeyDown(KeyCode.R))
        {
            myState = States.cell;
        }
    }
    void state_mirror()
    {
        text.text = "The mirror has been shattered leaving shards scattered across the floor." +
            "\n\nPress T to Take the mirror shards or R to return to cell";
        if (Input.GetKeyDown(KeyCode.R))     {myState = States.cell;}
        if (Input.GetKeyDown(KeyCode.T))     { myState = States.cell_mirror; }
    }
    void state_cell_mirror()
    {
        text.text = "You are still locked in your cell. There are some dirty " +
           "sheets on the bed and the prison cell door is still locked shut.\n\n" +
            "Press S to view Sheets or L to view Lock";
        if (Input.GetKeyDown(KeyCode.S)) { myState = States.sheets_1; }
        if (Input.GetKeyDown(KeyCode.L)) { myState = States.lock_1; }
        
    }
    void state_lock_1()
    {
        text.text = "You put the mirror shard you found earlier through the "+
            "bars and look at the front of the passcode lock. "+
            "One of the guards must've been eating cheetos. " +
            "You press the cheeto powdered buttons and hear a click.\n\n" +
            "Press O to Open";
        if (Input.GetKeyDown(KeyCode.O)) { myState = States.freedom; }
       
    }
    void state_sheets_1()
    {
        text.text = "Holding the mirror in your hand doesn't make the sheets any cleaner.\n\n" +
            "Press R to return to exploring your cell";
        if (Input.GetKeyDown(KeyCode.R)) { myState = States.cell_mirror; }
    }
    void state_freedom()
    {
        text.text = "You are free from your cell.\n\n " +
            "Press P to Play again";
        if (Input.GetKeyDown(KeyCode.P)) { myState = States.cell;}
    }
}


