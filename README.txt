========================================
 AutoQuestLearner
========================================

This is a STANDALONE addon. You do NOT need pfQuest, Questie-X, or
TomTom installed or enabled for this to work -- it's fully self-
contained on its own. If you happen to have TomTom installed too, it
can optionally use it; if not, everything still works without it.

Author: Ezinagro

Inspired by pfQuest (created by shagu) and Questie-X (maintained by
Xurkon, a fork of the original Questie project rebuilt for private
servers). A small number of quest NPC gaps are filled in from the
original Questie project (by Aero, Logon, Muehe, TheCrux/BreakBB,
Drejjmit, Dyaxler, Cheeq, TechnoHunter, and other contributors).
Precise "stand here" coordinates for zone-wide kill/interact
objectives are supplemented with data from TourGuideVanilla (by
cralor, credit to Tekkub for the original framework). Precise quest
giver and turn-in coordinates are further supplemented from additional
community leveling-guide data. A lot of work has gone into this -- compiling
and merging quest, NPC, and objective location data together from
multiple different community databases, scraping, and cross-
referencing sources to fill in the gaps that any single one of them
leaves on its own.

----------------------------------------
 INSTALLATION
----------------------------------------

1. Extract this zip.
2. Copy the "AutoQuestLearner" folder into your WoW/Ascension
   Interface\AddOns\ folder, so the final path looks like:
       ...\Interface\AddOns\AutoQuestLearner\AutoQuestLearner.toc
3. Fully restart the game client (not just /reload) the first time you
   install it.
4. At the character select screen or in-game, make sure the addon is
   enabled in your AddOns list.

----------------------------------------
 WHAT IT DOES
----------------------------------------

At its core, this addon learns as you (and everyone else using it)
play. Quest giver locations, turn-in NPC locations, and objective
locations all get saved to a shared learned database -- so if the
bundled data doesn't already know where something is, the addon fills
that gap in for your next leveling adventure, and it only gets more
complete over time as more of it gets played through.

Alliance and Horde are both supported.

Key features:
  - Built-in smart arrow -- points you toward your next quest
    objective or turn-in without needing a separate addon
  - Learns and saves quest giver, turn-in, and objective locations
    automatically as you play, filling in gaps in the bundled data
  - Available quest suggestions -- the arrow and map can also point
    you toward nearby quests you haven't picked up yet, not just
    what's already in your log. Filtered by level range, faction
    (a real bitwise check, not just whole-faction), actual completion
    history (checked against the server, not just this addon's own
    records), and known chain prerequisites, so it tries hard not to
    suggest something you can't actually take yet.
  - Quest item buttons -- a small movable panel shows the icon for any
    "use this on the objective" quest item (like an Essence Extractor)
    so you can use it with one click, same as from your bags
  - Travel routes -- for quests whose destination is in a different
    zone, shows a real hand-verified route (or points the arrow at an
    actual checkpoint, where a precise one is known) instead of a
    generic "fly or travel there"
  - In-game quest tracker (can replace Blizzard's default one)
  - Map and minimap nodes for quest givers and objectives
  - Route planner -- suggests an efficient order to tackle your
    active quests, clustering nearby quests together so you clear a
    whole area before backtracking
  - Zone completion tracking -- see how many known quests you've
    finished in your current zone
  - Quest chain preview -- shows the next quest in a chain when one
    is known, right when you're about to turn something in
  - TomTom integration (optional, if you have TomTom installed)

This addon is still a work in progress. Bugs and gaps in the location
data are expected -- if you find one, /aql learn (see below) helps fix
it permanently, for everyone using the shared database.

----------------------------------------
 IN-GAME GUIDE
----------------------------------------

Run /aql guide at any time for a full in-game explainer covering how
the arrow behaves, map/minimap icons, pinning a quest, and more detail
than this file goes into. It opens automatically the first time you
install the addon, too.

----------------------------------------
 SLASH COMMANDS
----------------------------------------

/aql
/aql status
    Prints a short status summary and this same command list in chat.

/aql guide
    Opens the in-game how-to-use guide.

/aql config
    Opens the settings panel (also: /aqlconfig). Has quick-access
    buttons along the top for Guide, Route, Zone, and Chain.

/aql route
    Suggests an order to tackle your active quests in your current
    zone, clustering nearby quests together so you clear one area
    before moving to the next, rather than backtracking repeatedly.

/aql zone
    Shows how many known quests you've completed in your current
    zone, and lists what's left.

/aql chain [quest name]
    Shows the next quest in the chain, if one is known. With no name
    given, uses your currently pinned quest.

/aql learn [quest name]
    Manually saves your current location as an objective (or turn-in,
    if the quest is complete) location for that quest. With no name
    given, uses whichever single quest is currently watched/tracked.
    This is the main way bad or missing location data gets corrected.

/aql db
    Detailed breakdown of how much the shared learned database
    currently knows -- quest count, NPC count, etc.

/aql opendb [questID]
    Opens that quest's page on the Ascension Database in your browser
    -- with a quest selected/open in your quest log, or a specific
    quest ID typed directly (e.g. "/aql opendb 641"). Requires this
    client's OpenAscensionDBURL function; not available everywhere.

/aql resync
    Force-reloads all learned locations and refreshes map nodes.

/aql scan
    Forces an immediate proximity scan for nearby quest givers.

/aql proximity
    Toggles automatic proximity-based objective learning on/off (on
    by default) -- this is what lets locations get learned just from
    being near an objective while questing, no kill/loot required.

/aql focus
    Toggles showing only what the arrow is currently tracking on the
    map/minimap, versus showing everything known nearby.

/aql tracker
    Toggles this addon's own quest tracker panel on/off.

/aql blizztracker
    Toggles Blizzard's default quest tracker on/off.

/aql map
    Forces an update of map nodes.

/aql unpin
    Clears a pinned quest, returning the arrow to auto-select mode.
    (Alt+Right-Click a tracked quest does the same thing, and pins one
    too.)

/aql tomtomauto
    Toggles automatically selecting the closest TomTom waypoint, if
    TomTom is installed.

/aql gossip
    Reprocesses the currently open gossip window (rarely needed
    manually -- mostly automatic).

/aql arrow
    Diagnostic -- explains exactly why the navigation arrow is or
    isn't showing right now, and what the addon currently knows about
    your active quests.

/aql questitems
    Diagnostic for the quest item button panel -- shows what's
    currently detected and why a button might not be appearing.

/aql debug
    Prints general diagnostic info.

Troubleshooting tools (not needed for normal play):

/aql flickerdebug
    Records for 5 seconds and reports exactly how many times various
    tracker functions fired -- useful if the tracker or map ever
    seems to flicker or refresh oddly.

/aql perf
    Quick memory usage check for this addon specifically.

/aql perfdebug
    Records for 10 seconds and reports real measured time spent in
    the functions most likely to affect FPS.

Mouse actions:
  Alt+Right-Click a tracked quest  - pin/unpin the arrow to that quest
  Alt+Click a tracked quest        - set a TomTom waypoint (if enabled)

----------------------------------------

Thanks for testing -- feedback on anything broken, missing, or
confusing is always welcome.
Email Ezinagro1985@gmail.com       for any info ty for testing I am trying to put the time into this to help...