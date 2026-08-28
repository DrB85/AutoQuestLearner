========================================
 AutoQuestLearner
========================================

This is a STANDALONE addon. You do NOT need pfQuest or Questie-X
installed or enabled for this to work -- it's fully self-contained
on its own.

Author: Ezinagro

Inspired by pfQuest (created by shagu) and Questie-X (maintained by
Xurkon, a fork of the original Questie project rebuilt for private
servers). A small number of quest NPC gaps are filled in from the
original Questie project (by Aero, Logon, Muehe, TheCrux/BreakBB,
Drejjmit, Dyaxler, Cheeq, TechnoHunter, and other contributors).
Precise "stand here" coordinates for zone-wide kill/interact
objectives are supplemented with data from TourGuideVanilla (by
cralor, credit to Tekkub for the original framework).

A lot of what powers this addon comes from projects that had gone
quiet -- community databases nobody had cross-checked in years, NPC
data compiled by contributors long since moved on, coordinates nobody
had gone back to audit. The work here has been less about starting
from scratch and more about doing the maintenance those projects
needed: validating old data against independent sources (including
authentic client data pulled directly from a real 3.3.5a build, and
creature spawn data cross-checked against three separate independently-
sourced databases), pulling exact figures from real game files instead
of estimating, and fixing what had quietly drifted wrong.

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

Quest titles, descriptions, objectives, NPC names, and zone names are
also available in German, French, Korean, Portuguese, Russian, Spanish
(both regional variants), and Chinese (both Simplified and
Traditional) -- automatically matched to your client's own language,
with graceful fallback to English for anything a given language's data
doesn't cover yet. The addon's own interface text (command output,
tooltips, notifications) is still English-only for now.

If the arrow has genuinely nothing to go on for a specific quest --
not in the bundled data, nothing learned yet by anyone -- it says so
plainly for a confirmed small set of these cases instead of silently
going blank, and explains that finding it in-game teaches the addon
(and every other player) its location automatically. This doesn't
change how learning works at all; it's the same automatic process as
everything else this addon learns, just with a clearer explanation
while the gap still exists.

Key features:
  - Built-in smart arrow -- points you toward your next quest
    objective or turn-in without needing a separate addon, and now
    shows the actual objective description underneath the target name
    (not just "find X nearby") so unusual objectives -- a boss that
    must be summoned first, an item that must be used on something --
    are actually explained, not just pointed at
  - Learns and saves quest giver, turn-in, and objective locations
    automatically as you play, filling in gaps in the bundled data --
    even just targeting an NPC you haven't dealt with yet can teach
    its location, if it's a known giver/turn-in for something. Learned
    positions keep refining toward the most recently confirmed spot
    rather than staying frozen at wherever they were first recorded
  - Available quest suggestions -- the arrow and map can also point
    you toward nearby quests you haven't picked up yet, not just
    what's already in your log. While your log still has quests,
    the arrow prioritizes objectives/turn-ins only (no lock on the
    giver or random targeted NPC at Distance 0.0). Filtered by level range, faction
    (a real bitwise check, not just whole-faction), actual completion
    history (checked against the server, not just this addon's own
    records), reputation requirements, PvP-flag requirements, and
    known chain prerequisites -- including "must complete ALL of
    these", "must complete ANY ONE of these", "only available while a
    specific other quest is active", and "mutually exclusive with a
    sibling quest" -- so it tries hard not to suggest something you
    can't actually take yet. Quests that need a specific item already
    in hand before they'll even let you interact are also correctly
    held back until you actually have it. If you're already actively
    pursuing a real, known objective, an unrelated available quest has
    to be genuinely close by to interrupt that, not just marginally
    closer by chance
  - Class-restricted quests aren't suggested for pickup by default,
    even for a matching class, since this server's custom class roster
    means this addon can't reliably verify extra requirements those
    quests often carry (toggle with /aql trackclassquests if you want
    them suggested anyway)
  - Handles quest IDs this server has repurposed for entirely
    different custom content than the original vanilla quest that
    number used to mean -- detected automatically by comparing your
    live quest title against this addon's own bundled data, with a
    manually-verified correction available for confirmed cases rather
    than just losing all location data for them
  - Quest item tooltip progress -- hover any quest-relevant item
    anywhere (bags, the ground, a vendor) to see which quest needs it
    and your current progress, color-coded by completion
  - Announce quest accept/complete/abandon and kill/loot progress to
    party/raid chat, independently toggleable, off by default
  - Live, in-game summary of how much the shared database actually
    knows so far -- shown automatically on login, or check anytime
  - Share what you've learned with other players -- live sync with
    party/raid/guild in real time, or /aql export and /aql import for
    trading your whole learned history with someone anytime, no
    grouping required
  - Quest item buttons -- a small movable panel shows the icon for any
    "use this on the objective" quest item (like an Essence Extractor)
    so you can use it with one click, same as from your bags
  - Travel routes -- for quests whose destination is in a different
    zone, shows a real hand-verified route (or points the arrow at an
    actual checkpoint, where a precise one is known) instead of a
    generic "fly or travel there"
  - In-game quest tracker (can replace Blizzard's default one), with
    an optional position/size lock so it can't be accidentally dragged
  - Map and minimap nodes for quest givers and objectives -- kill/loot
    objective spawn areas can optionally show as a shaded area instead
    of a dot cluster (Outline Spawn Areas, off by default, in
    /aql config) for whichever quest the arrow is currently tracking.
    Gathering nodes (herbs, ore, etc.) always keep precise individual
    dots regardless of this setting, since a fixed resource node isn't
    the same thing as a wandering creature's general hunting ground
  - Route planner -- suggests an efficient order to tackle your
    active quests, clustering nearby quests together so you clear a
    whole area before backtracking
  - Zone completion tracking -- see how many known quests you've
    finished in your current zone
  - Quest chain preview -- shows the next quest in a chain when one
    is known, right when you're about to turn something in

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

The essentials -- everything most people ever need:

/aql
/aql status
    Prints a short status summary and the essential command list in
    chat. /aql help all shows every command, including the more
    advanced/rarely-needed ones -- most people will never need that
    longer list.

/aql guide
    Opens the in-game how-to-use guide.

/aql config
    Opens the settings panel (also: /aqlconfig). Has quick-access
    buttons along the top for Guide, Route, Zone, and Chain.

/aql learn [quest name]
    Manually saves your current location as an objective (or turn-in,
    if the quest is complete) location for that quest. With no name
    given, uses whichever single quest is currently watched/tracked.
    This is the main way bad or missing location data gets corrected.

/aql missing
    Report that a quest giver the arrow just sent you to genuinely
    isn't there -- run it while standing on the spot. No addon can
    check "does an NPC exist here" from a distance on this client, so
    this is the only way that gap ever gets closed: it stops
    suggesting that quest at that location.

/aql sleep [questID]
/aql wake [questID]
    Pull an available (not-yet-picked-up) quest out of rotation
    entirely, on every character on your account, until you wake it
    back up. Useful for a quest you know is wrong or don't want
    suggested right now.

/aql sync
    Check location-sharing status with party/raid/guild, and how many
    locations you've received/applied this session.

/aql export
    Get a copyable text string of everything you've learned, to share
    with another player running this addon.

/aql import
    Paste someone else's export string to add their learned locations
    to yours. Never overwrites anything you already have.

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

/aql suggestzone
    Suggests which zone(s) to level in next, based on your level,
    race, and faction, following the same zone progression established
    Classic leveling guides use (not just raw known-quest counts) --
    with known-location quest coverage shown alongside each suggestion
    so you can see how well-mapped that zone actually is.

/aql tracker
    Toggles this addon's own quest tracker panel on/off.

/aql unpin
    Clears a pinned quest, returning the arrow to auto-select mode.
    (Alt+Right-Click a tracked quest does the same thing, and pins one
    too.)

----------------------------------------

More settings and tools -- useful, but not needed day-to-day:

/aql db
    Detailed breakdown of how much the shared learned database
    currently knows -- quest count, NPC count, etc.

/aql learnedstats
    Shows how much the shared learned database actually knows so far
    (account-wide, every character on your account combined) -- quest
    giver/turn-in locations, objectives with spawn data, total spawn
    points.

/aql floor up|down|clear
    While standing on an unresolved pin (the arrow warns "coordinates
    can't tell floors apart"), teach it which way the real target
    actually is -- applies to that whole objective's spawn cluster
    when it's an objective, not just the one pin. "clear" removes a
    previously-given hint.

/aql proximity
    Toggles automatic proximity-based objective learning on/off (on
    by default) -- this is what lets locations get learned just from
    being near an objective while questing, no kill/loot required.

/aql focus
    Toggles showing only what the arrow is currently tracking on the
    map/minimap, versus showing everything known nearby.

/aql blizztracker
    Toggles Blizzard's default quest tracker on/off.

/aql map
    Forces an update of map nodes.

/aql scan
    Forces an immediate proximity scan for nearby quest givers.

/aql opendb [questID]
    Opens that quest's page on the Ascension Database in your browser
    -- with a quest selected/open in your quest log, or a specific
    quest ID typed directly (e.g. "/aql opendb 641"). Requires this
    client's OpenAscensionDBURL function; not available everywhere.

/aql announceparty
    Toggles announcing quest accept/complete/abandon in party/raid
    chat (off by default).

/aql announcepartyprogress
    Toggles announcing kill/loot progress (e.g. "4/8") in party/raid
    chat (off by default, separate from the above).

/aql questitemtooltip
    Toggles showing quest progress on item tooltips, anywhere an item
    tooltip shows up (on by default).

/aql lock
    Toggles locking the tracker's position/size so it can't be
    accidentally dragged or resized (off by default).

/aql availrange [number]
    View or set how far the arrow will look for an available quest to
    auto-suggest (default 20, smaller = only very nearby ones).

/aql availrangeactive [number]
    Same, but specifically while you already have a real active-quest
    objective to head toward (default 5, tighter than the above -- an
    available pickup only competes if genuinely close by).

----------------------------------------

Advanced / rarely needed -- most people will never touch these:

/aql learnnotify
    Toggles the automatic "Learned a new spawn point" chat
    notification on/off (on by default).

/aql learnedstatsauto
    Toggles showing the /aql learnedstats summary automatically every
    login/reload (on by default), so you can watch it grow as you play.

/aql trackascension
    Toggles whether Ascension's own custom-added quests (not part of
    the original vanilla quest set) get suggested for pickup at all
    (off by default).

/aql trackclassquests
    Toggles whether class-restricted quests get suggested for pickup
    at all, even for a matching class (off by default -- see the note
    on class restrictions above).

/aql zonenudge
    Toggles the one-time-per-zone nudge suggesting where to go next
    once a zone's known quests are mostly done.

/aql zonefilter
    Toggles whether the tracker only shows quests from your current
    zone, or everything across all zones.

/aql pvprequired [clear]
    Shows PvP-flag-required quests this addon has learned about from
    the game's own error messages. "clear" resets the learned list.

/aql reprequired [clear]
    Same, for reputation-gated quests learned the same way.

/aql unavailable [clear]
    Shows quests this addon has learned are genuinely unavailable
    (via /aql missing reports or in-game confirmation), so they stop
    being suggested. "clear" resets the learned list.

/aql respawntimers [clear]
    Shows personally-learned respawn timers for creatures you've
    killed and watched respawn. "clear" resets them, falling back to
    vanilla-sourced defaults or a flat guess.

/aql backfillids
    One-time (re-runnable) pass tagging NPC identity onto previously-
    learned spawn points where the source is unambiguous, so they can
    be individually hidden on kill the same way freshly-learned ones
    already are.

/aql resync
    Force-reloads all learned locations and refreshes map nodes.

/aql gossip
    Reprocesses the currently open gossip window (rarely needed
    manually -- mostly automatic).

/aql calibrate [reset]
    Shows minimap-scale calibration progress for the starting-zone
    sub-areas that need it (Shadowglen, Coldridge Valley, Camp Narache,
    Red Cloud Mesa, Deathknell, Valley of Trials) -- these get
    self-measured from your actual movement rather than relying on
    static data, since no external database has this exact value for
    them. Most of these start with a real (though not client-verified)
    estimate from a modern client's own zone data as an interim value
    while self-calibration is still collecting samples; that self-
    measured value always takes over once it's ready. "/aql calibrate
    reset" re-measures your current zone if needed.

----------------------------------------

Diagnostic / troubleshooting -- not needed for normal play:

/aql arrow
    Explains exactly why the navigation arrow is or isn't showing
    right now, and what the addon currently knows about your active
    quests.

/aql why [questID]
    Full gating breakdown for why an available quest is or isn't being
    suggested for pickup (prerequisites, exclusion groups, completion
    history, etc.), with a quest selected/open in your quest log, or a
    specific quest ID typed directly.

/aql questitems
    Diagnostic for the quest item button panel -- shows what's
    currently detected and why a button might not be appearing.

/aql debug
    Prints general diagnostic info.

/aql debuglog
    Toggles internal diagnostic logging to chat (off by default).

/aql killdebug
    Toggles kill-tracking debug -- every kill prints what NPC ID was
    parsed and whether a matching map node was found/hidden.

/aql clusterdebug
    Toggles a visual debug overlay on the world map for cluster
    merging.

/aql flickerdebug
    Records for 5 seconds and reports exactly how many times various
    tracker functions fired -- useful if the tracker or map ever
    seems to flicker or refresh oddly.

/aql perf
    Quick memory usage check for this addon specifically.

/aql perfdebug
    Records for 10 seconds and reports real measured time spent in
    the functions most likely to affect FPS.

----------------------------------------

Mouse actions:
  Alt+Right-Click a tracked quest  - pin/unpin the arrow to that quest

----------------------------------------
 TIP: PUT /aql learn, /aql missing, AND /aql sleep ON A KEYBIND
----------------------------------------

These three only actually help if you use them the moment you notice
something wrong -- and typing a full command out while standing on
the spot is exactly the kind of friction that makes people just shrug
and move on instead of fixing it. Turning each into a one-key macro
removes that friction:

1. Type /macro (or Game Menu -> Macros) to open the Macros window.
2. Click New, give it any name and icon.
3. Type one command as the entire body, e.g. just:
       /aql learn
   on its own line.
4. Drag the macro onto an action bar, then bind a key to it (Game
   Menu -> Key Bindings, or Shift-drag it directly onto the bar).

Repeat for /aql missing and /aql sleep as their own separate
macros/keys. Once bound, correcting bad data on the spot is a single
keypress -- and since the data is shared, every correction helps
everyone else using this addon too, not just you.

----------------------------------------


----------------------------------------
 CHANGELOG (August 28, 2026)
----------------------------------------

Arrow / navigation
  - Fixed the arrow locking onto any targeted NPC (vendors, trainers,
    books, quest givers) as "(available)" at Distance 0.0 until you
    walked out of range. Available targets now only come from the
    real quest-giver database, not from your current target.
  - While your quest log has any quests, the arrow no longer suggests
    available pickups -- it stays on objectives and turn-ins. Available
    suggestions return when the log is empty.
  - Fixed a math bug where "skip available" still matched nearby givers
    (maxRange -1 squared to 1). Available is fully skipped when the log
    has work.
  - TomTom-style clear on accept and quest-log change: drop the old
    waypoint, refresh the log, retarget immediately -- works with other
    auto-accept addons that never fire QUEST_ACCEPTED for us.
  - On accept, ClearTarget() so the arrow is not glued to the NPC.
  - Session arrow/available cache purged on login (no cross-character
    leftovers).
  - Faster retarget after accept/turn-in; force path runs near-instantly.

Minimap / starting zones
  - Coldridge Valley (and other starting sub-zones) no longer use the
    parent zone's yard size for minimap scale -- that caused clusters to
    crawl as you walked.
  - Auto minimap-scale calibration kicks on login and zone change so
    starting areas remeasure in the background.

Map / tracker
  - Same-coord cluster dedupe: Ascension + pfQuest + learned pins at the
    same spot collapse to one ring instead of stacked rings.
  - Tracker objectives show a colored dot matching the minimap ring
    color for that objective, so you can match tracker lines to map
    nodes at a glance.

Performance
  - Coalesced map/tracker rebuilds on kill, loot, accept, turn-in, and
    zone change to cut FPS stutters.
  - Throttled available-giver cache, minimap updates, and route dots.

Thanks for testing -- feedback on anything broken, missing, or
confusing is always welcome.
Email Ezinagro1985@gmail.com       for any info ty for testing I am trying to put the time into this to help...