# Explanation of `callalliesisvalid` Country Events

The provided code defines three country events within the `callalliesisvalid` namespace.

- Steam Workshop: https://steamcommunity.com/sharedfiles/filedetails/?id=3492212054

## Event 1: `callalliesisvalid.1`

### Purpose
This event triggers when Ottomans (`TUR`) is involved in an offensive war and has not yet called its allies. It prompts Ottomans to call all subject countries (e.g., vassals, allies, or puppets) to join its offensive wars.

### Structure
- **Namespace**: `callalliesisvalid`
- **ID**: `callalliesisvalid.1`
- **Title**: `callalliesisvalid.1.t` (references a localized string for the event title)
- **Description**: `callalliesisvalid.1.d` (references a localized string for the event description)
- **Picture**: `LAND_MILITARY_eventPicture` (displays a military-themed event image)

### Trigger Conditions
The event fires if:
- The country is Ottomans (`tag = TUR`).
- Ottomans is in an offensive war (`is_in_war = { attackers = TUR }`).
- The country does not have the `war` flag (`NOT = { has_country_flag = war }`).

### Immediate Effects
- Sets the `war` country flag (`set_country_flag = war`), marking that Ottomans has initiated the process of calling allies.

### Options
- **Option Name**: `callalliesisvalid.1.a` (references a localized string for the option text)
- **Effect**: All subject countries of Ottomans (`every_subject_country`) join all of Ottomans's offensive wars (`join_all_offensive_wars_of = TUR`).

### Summary
This event represents Ottomans rallying its subject nations to join an ongoing offensive war, ensuring they participate in the conflict. The `war` flag prevents the event from firing repeatedly during the same war.

## Event 2: `callalliesisvalid.2`

### Purpose
This event triggers when Ottomans is no longer in an offensive war but has the `war` flag from the previous event. It serves as a transition to clear the `war` flag and initiate a follow-up event.

### Structure
- **Namespace**: `callalliesisvalid`
- **ID**: `callalliesisvalid.2`
- **Title**: `callalliesisvalid.2.t` (references a localized string for the event title)
- **Description**: `callalliesisvalid.2.d` (references a localized string for the event description)
- **Picture**: `LAND_MILITARY_eventPicture` (uses the same military-themed image as Event 1)

### Trigger Conditions
The event fires if:
- The country is Ottomans (`tag = TUR`).
- Ottomans is not in an offensive war (`NOT = { is_in_war = { attackers = TUR } }`).
- The country has the `war` flag (`has_country_flag = war`), indicating it previously called allies into a war.

### Immediate Effects
- Clears the `war` country flag (`clr_country_flag = war`), resetting the war state.

### Options
- **Option Name**: `callalliesisvalid.2.a` (references a localized string for the option text)
- **Effect**: Triggers another event with ID `callalliesisvalid.3` (`country_event = { id = callalliesisvalid.3 }`).

### Summary
This event acts as a cleanup mechanism when Ottomans’s offensive war ends, clearing the `war` flag and triggering a follow-up event to handle post-war effects, such as a peace celebration or acknowledgment.

## Event 3: `callalliesisvalid.3`

### Purpose
This event represents a post-war scenario, likely a victory parade or peace celebration, triggered only when called by Event 2 and when Ottomans is not in an offensive war. It sets a `peace` flag to mark the resolution of the war cycle.

### Structure
- **Namespace**: `callalliesisvalid`
- **ID**: `callalliesisvalid.3`
- **Title**: `callalliesisvalid.3.t` (references a localized string for the event title)
- **Description**: `callalliesisvalid.3.d` (references a localized string for the event description)
- **Picture**: `GFX_evt_parade` (displays a parade-themed event image, suggesting a celebratory or ceremonial event)

### Trigger Conditions
- **Triggered Only**: The event only fires when explicitly called by another event (`is_triggered_only = yes`), in this case, by Event 2.
- The country is Ottomans (`tag = TUR`).
- Ottomans is not in an offensive war (`NOT = { is_in_war = { attackers = TUR } }`).
- The country does not have the `peace` flag (`NOT = { has_country_flag = peace }`), preventing the event from firing repeatedly.

### Immediate Effects
- Sets the `peace` country flag (`set_country_flag = peace`), marking the post-war state.

### Options
- **Option Name**: `callalliesisvalid.3.a` (references a localized string for the option text)
- **Effect**: No additional effects are specified, suggesting this option may simply acknowledge the event (e.g., "OK" or "Celebrate").

### Summary
This event serves as a concluding event in the sequence, likely representing a ceremonial or narrative conclusion to the war, such as a victory parade. The `peace` flag ensures the event does not repeat unnecessarily.

## Overall Flow
1. **Event 1 (`callalliesisvalid.1`)**: Triggers when Ottomans starts an offensive war, calls subject countries to join, and sets the `war` flag.
2. **Event 2 (`callalliesisvalid.2`)**: Triggers when the offensive war ends, clears the `war` flag, and initiates Event 3.
3. **Event 3 (`callalliesisvalid.3`)**: Triggers to mark the post-war state with a `peace` flag, likely representing a narrative conclusion like a parade.

## Notes
- The events rely on localized strings (e.g., `callalliesisvalid.1.t`, `callalliesisvalid.1.d`) defined elsewhere in the mod’s localization files.
- The use of flags (`war`, `peace`) ensures the events fire in the correct sequence and do not repeat unnecessarily.
- The events are specific to Ottomans (`TUR`) and its offensive wars, suggesting a mod focused on Ottomans’s historical or alternate-history role.
- The `every_subject_country` scope in Event 1 implies Ottomans has subjects (e.g., puppets or vassals) that can be called into war, which may depend on the game’s mechanics or mod setup.

This event chain provides a structured narrative for Ottomans’s involvement in offensive wars, from rallying allies to celebrating peace, enhancing the gameplay experience with thematic flavor.

## Sources

- https://eu4.paradoxwikis.com/Triggers
- https://eu4.paradoxwikis.com/Scopes
- https://eu4.paradoxwikis.com/Effects
- https://eu4.paradoxwikis.com/Event_modding
