Scenes:
    TopDownDemo - Demo scene of Topdown in 2D (Main)
    TopDownDemo - Demo scene of Topdown in 3D

Main Scene Objects:
    Main Camera
    Managers
    CharacterTopDown (Player)
        Components:
            Transform - Editable
            Sprite Renderer - Editable
            Animator - Editable
            Rigidbody 2D - Editable
            Capsule Collider 2D - Editable
            Player Character (Script) - Editable
            Auto Order Layer (Script) - Editable
            Character Anim (Script)
            Character Hold Item (Script) - Editable
        Hand
        Shadow
    Scene
        Floor (Prefab)
        Walls (Prefab)
        Levers (Prefab)
        Doors (Prefab)
        DoorKeys (Prefab)
        Shadows (Prefab)
        Grass1 (Prefab) 
        Grass2 (Prefab) 
    Lights
        Directinal light
        Point lights

Scripts
    AutoOrderLayer.cs - This script automatically updates the sorting order and X rotation, so that it faces the camera and sort based on the Y value
    AutoOrderLayerChild.cs - This script automatically updates the sorting order and X rotation, so that it faces the camera and sort based on the Y value for child objects 
    Carryltem.cs - Class that defines carriable items and allows character to pick it up   
    CharacterAnim.cs - Transfers characters information to animator
    CharacterHoldltem.cs - Controls characters holded item
    Door.cs - Defines unlockable door and is letting character to open it 
    FixOffset.cs - Fixes Z offsets to offset all the assets with this script in the scene
    FollowCamera.cs - Makes camera follow character
    Key.cs - Defines key to open door
    Lever.cs - Defines lever to interact with
    PlayerCharacter.cs - Character movement script
    PlayerControls.cs - Player controls settings
    Sprite3D.cs - Allow using Sorting Layer and Sorting Order on 3D MeshRenderers
    TheAudio.cs - Main script for playing audio