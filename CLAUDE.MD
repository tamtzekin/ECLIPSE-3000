## Agent Roles

When working on complex tasks, use these specialized approaches:

### Level Design Tasks
Focus on actor placement, lighting, post-processing, and scene composition.
<!-- Use the Unreal MCP tools for all editor operations. -->
Always check that new actors follow our naming conventions.
Save the level after significant changes.

SCENE CHAPTERS:

CHARACTERS:
- All talkable NPCs should not be moving.
- Move the Bouncer to stand in front of the VIP Room entrance (Behind the Cloak Room Desk)
- Move the Cloakroom Lady to behind the Cloakroom, standing and not moving.

SMOKING SECTION
- ~~groups of people standing around, talking, smoking . not walking around.~~ DONE (stationary NPCs in smoking rooms)
- ~~add a single smoke rising animation, doesnt have to be complicated, just a gradient line flowing up and fading out~~ DONE (3 animated rising smoke columns)
- ~~red light~~ DONE (red PointLight in smoking area)

LEVEL DESIGN: CLUB ROOM- the stage has a small step, you step up onto the floor
- ~~the dancefloor needs some sort of floor collider that means the characters aren’t clipping through~~ DONE (player + NPCs raised 0.4 when on dance platform)
- ~~add a lot more poeple to the CLUB ROOM, make it feel packed~~ DONE (25-35 NPCs + 5-7 crowds)

LEVEL DESIGN: ALL
- Many of the rooms, when you enter, they have a really tight space between the new room and the enter/exit point between rooms. It means I often move and accidentally go back to the other room. Add more space between each level's entrance and the space in front (ie. not putting objects right in front of an entrance in a new room)

LEVEL DESIGN: BAR ROOM 
- ~~Add a dialogue tree to the BARTENDER.~~ DONE (Dlg_Bartender 0x0D00, [PLACEHOLDER DIALOGUE])
- ~~The second option is ‘Can I  get a drink?’ Bartender: ‘You’re supposed to tell me what you want.’~~ DONE
- ~~The third option [Leave] I changed my mind. Thanks. ‘The bartender says nothing. Her eyes are already on someone else.’~~ DONE
- ~~Add some spirit bottles in front of stands backlit with amber light. Some beer taps. A bar with a sink. A box of limes. A cutting board with a knife on it. All low poly.~~ DONE (6 bottles, amber backlight, 3 taps, sink, lime box, cutting board + knife)
- ~~The bar should be its own room, separate to the Cloak Room (which is the FIRST room. Long, not square).~~ DONE (BAR_ROOM='0,1' separate from COAT_CHECK_ROOM='0,0') 


SHOP MECHANIC: ORDERING AT BAR
- At the bar, right now, there are two separate things, 'Order at Bar' and '[E] Bartender'. I would like this interaction to be through the Bartender. ie. You talk to the bartender, it opens up a dialogue tree, where one of the options is "Show me what you've got" - this dialogue choice opens the bar's 'sell' menu

ITEM PICKUP
- when you are near an item, or hover over it, outline it blue. Then, show [PICK UP x item] (in the same UI styling that you have "[E] Order at Bar")


LEVEL DESIGN: VIP ROOM
- ~~When you sit, you enter a conversation with the people sitting on the sofa.~~ DONE (opens dialogue with booth NPC)
- the mirrors ar enot reflecting the objects and NPCs in the room. reflective PlaneGeometry, shininess:300 are you using this?
- Add a character (‘Jordi’). This foreigner who is a stylist and trades in fashion. You can sell him clothes for cash. Jordi should be sitting at a red booth. He is talkable to when you choose Sit Down action. (Jordi NPC in VIP, sell menu with prices, Articy dialogue 0x0E00) 

LEVEL DESIGN: BATHROOM
- ~~you can’t enter into stalls that are closed~~ DONE (collision on closed stall doors)
- no strobing light in the bathroom, only dark bold blue
- move the Red Wristband to the other side of the sink, closer to the toilet stalls. And show it as a red circle object (low poly ofc)

### UI Design Tasks
Focus on designing and implementing UI, performance is smooth, keeping with existing fonts and colours, follows existing UX patterns. 

UI DESIGN: BAR AND CLOAK ROOM MENUS
- ~~The Cloak Room item menu is just dialogue. [Hand over Cloakroom ticket #number”] You don’t see what item you get, or their benefit.  Remove the shop-like interface from the Cloak Room~~ DONE
- ~~You can use number keys to instantly buy the item assigned to that number. Display next to the names as Hotkey tips.~~ DONE

UI DESIGN: INTERACT WITH ENVIRONMENT OBJECTS
- ~~holding TAB highlights interactable/pickup-able objects with a light blue outline~~ DONE (cyan emissive glow on all interactMeshes while TAB held)


### Game Mechanics Tasks
Focus on re-using existing design patterns and code patterns to keep it lean. Don't do unnecessary compute-heavy things like number generation or algorithms where not necessary. eg. Dice roll checks, keep them simple. 


TIME
- ~~You can try failed skill checks again in the next chapters, they reset on each chapter start.~~ DONE
- ~~Characters change room each chapter.~~ DONE (30% chance each NPC moves on chapter transition)
RAIN
- ~~Sometimes it rains, the smoking section becomes less populated (Czech Girls move into the VIP Room)~~ DONE (40% rain chance/chapter, Czech Girls relocate, NPCs hide)
- ~~The front outside also rains.~~ DONE (rain FX overlay on outdoor rooms, faster heat drop in rain) 
CHARACTER MOVEMENT/LEVEL DESIGN 
- ~~when pushing through crowd, move slower~~ DONE (0.4x speed in crowds)
CLOTHES MECHANIC
- ~~DIsplay a message to show that you can’t hold any more items.~~ DONE ("Inventory full!")

HEAT MECHANIC
- ~~instead of setting a minimum of 60% Heat to go outside, you can go out whenever you’re above 50%. when you do, your Heat starts dropping.~~ DONE (heatThreshold=50)
- ~~When your Heat is 0, you can’t talk to anyone, you’re too cold to talk.~~ DONE (cold talk block + "It’s cold. I need to go inside." + icy screen pulse + stagger movement)
- ~~OVERHEATING - when overheated, move a little bit faster. right now its too slow. where can I find that variable?~~ DONE (up to 1.3x at heat=100)
- ~~When standing still, HEAT drops slowly.~~ DONE (stationary cooling)
- ~~When moving, increase the HEAT slower. Right now it;’s increaisng too fast.~~ DONE (3 → 1.5/s)
- ~~Outside, heat drops slowe.r Right onw it;’s  too fast.~~ DONE (8 → 4/s)
- ~~When wearing items with more HEAT, your HEAT meter drops more slowly. ie. Jacket and Hoodie would keep you heated for longer. Just a scarf would be a bit less. Create a way for this to work, maybe as a multipler? eg. Heat reduction is at x0.75 times.~~ DONE (heatGainMult/coolRate per clothing item)


CLOTHES ‘HOLD’ SLOTS:
- ~~You have one for head, one for jacket, one for pants, one for shoes~~ DONE (4 typed slots: head/jacket/pants/shoes, clothing auto-assigns to matching slot)

DUMP CLOTHES BEHIND SPEAKER MECHANIC
- ~~You can pick them back up. using Q again.~~ DONE (Q discards, items re-pickable)
- ~~Adding an item adds it to the environment, in a pile behind the speaker.~~ DONE
- ~~Change the message to ‘Drop [insert: currently equipped clothing] behind speaker’~~ DONE (dynamic prompt + flash)

THIRST MECHANIC
- ~~talking decreases thirst a bit slower, too. right now you can only really have one conversation before becoming out of THIRST~~ DONE (3 → 1.5 per choice)


### Sound Design Tasks
Focus on clear audio that runs at a low but nice-sounding bitrate (.ogg files are best), when live audio effects are used (eg. EQ) focus on the specified effects rather than importing entire libraries.

SOUND DESIGN: MAIN CLUB ROOM:
- ~~the sound gets blown out in the lows (EQ)~~ DONE (lowshelf +8dB at 200Hz)
~~add a compressor (is this available in the audio engine im using? if not, dont install another library for it)~~ DONE (Web Audio DynamicsCompressorNode, no external lib)


### Dialogue Design Tasks
Focus on optimization with Articy, use variables to track different state rather than huge branching trees, 

DIALOGUE DESIGN
- Each NPCS has their own unique dialogue tree. It is unique to them. You should not reuse any dialogue tree on any NPC. They should not shuffle per room. Eg. Bartender should only be Bartender dialogue. Bouncer should only be Bouncer. No duplicates. 

### Performance Tasks
Start by profiling before making changes.
Focus on frame time, draw calls, triangle count, and memory usage.
Document all changes and their measured impact.
Never sacrifice gameplay-critical features for performance.

### Asset Pipeline Tasks
Use Unreal MCP tools.
Follow naming conventions for exports.
Verify Nanite compatibility for environment meshes.
Check UV layouts before export.