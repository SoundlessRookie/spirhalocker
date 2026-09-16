# Product
A web application where users can create, manage, and discover loadouts from "Splatoon: Raiders".

The application allows players to manually configure their loadouts, which consist of a weapon and its associated weapon powers, a tank type, up to 3 gadgets and their equipped gadget parts, and up to 5 relic powers. Users can keep loadouts private or publish them for other players to discover.

The application is not directly integrated with "Splatoon: Raiders" in the initial version. Players manually enter and configure their loadouts. If resources permit, then the application will slightly integrate with the game by allowing players to create a build from an in-game screenshot.
# Personas
## Anonymous visitor
- Can browse and view public loadouts.
- Can create a loadout to share by passing parameters into the URL, but is not saved.
- Does not have an account.
## Registered user
- Can create and manage their own loadouts.
- Can maintain information about their available and unlocked equipment.
- Can import and modify loadouts.
- Has an account.
# Core User Stories
## Anonymous Visitor
- I want to browse public loadouts so I can discover useful builds without creating account.
- I want to view a public loadout so I can inspect its configuration.
- I want to share a loadout using a direct link.
## Registered User
### Loadout Management
- I want to create a loadout so I can save my preferred gear configuration.
- I want to edit my own loadouts so I can change their configuration.
- I want to delete my own loadouts so I can remove builds I no longer need.
- I want to make my loadout public so other players can discover it.
- I want to make my loadout private so it is no longer publicly discoverable.
### Equipment Management
- I want to keep track of my favorite weapons.
- I want to keep track of my unlocked Gadgets and Gadget Parts.
- I want to keep track of my number of unlocked Gadget Part slots.
- I want to set loadout constraints based on the equipment and slots I have access to.
### Loadout Import
- I want to import a loadout that someone else published so I can use it as a starting point for my own build.
- I want to import a loadout from an in-game screenshot so I can recreate a build without manually entering every component.
### Build Assistance
- I want to receive build suggestions based on my registered weapons and unlocked Gadget Parts.
# Functional Requirements
## Accounts
- Users must be able to create an account.
- Users must be able to authenticate to their account.
- Users must be able to sign out.
- Users must be able to delete their account.
- Users must be able to enable and disable the visibility of AI features on their account.
- Accounts must be created with AI features disabled by default.
- Users must only be able to modify their own user data and loadouts.
## Loadouts
- A loadout must have a unique identifier.
- A loadout must belong to exactly one registered user.
- A loadout must have a visibility state of either public or private.
- A loadout must contain exactly one weapon.
- A loadout must contain zero to three weapon powers.
- A loadout must contain exactly one tank type.
- A loadout must contain zero to three gadgets.
- A loadout may only allow one gadget to match a different tank's type. For a Speed tank, this is a Tactical gadget. For a Power tank, this is a Speed gadget. For a Tactical tank, this is a Power gadget.
- A loadout must contain zero to five relic powers.
- A loadout may only allow one relic power to match a different tank's type. For a Speed tank, this is a Tactical relic power. For a Power tank, this is a Speed relic power. For a Tactical tank, this is a Power relic power.
- Users must be able to create, retrieve, update, and delete their own loadouts.
- Public loadouts must be viewable by any user.
- Private loadouts must only be viewable by their owner.
- Public loadouts must be accessible through a shareable URL.
## Equipment Management
TODO
## Loadout Import
TODO
## Anything else
TODO
# Domain Rules
## Loadout
TODO
## Weapon
- A loadout has exactly one weapon.
- A weapon has a type, level, rarity, and a brief description.
- A weapon's level ranges from 1 through 100.
- A weapon's rarity ranges from 1 through 5.
- A weapon's description mirrors its in-game description.
- A weapon has one or more damage fields, depending on the weapon's type.
  - Example: A Charger weapon has a "Full charge" field and a "Minimum charge" field.
- A weapon has a damage value per damage field, depending on the weapon's type and level.
- A weapon may optionally have the "Primo" prefix, which maximizes the stat it's optimized for.
  - The "Primo" prefix is only available for weapons with a rarity of 4 or 5.
- A weapon has a description, which depends on the weapon's type and the existence of the "Primo" prefix.
- A weapon has zero to three weapon powers.
  - A weapon with a rarity of 1 always has zero weapon powers.
  - A weapon with a rarity of 2 always has one weapon power.
  - A weapon with a rarity of 3 has one or two weapon powers.
  - A weapon with a rarity of 4 has two or three weapon powers.
  - A weapon with a rarity of 5 always has three weapon powers.
## Weapon Power
- A weapon power has a type and a level.
- A weapon power's level ranges from 1 through 3.
- A weapon power has a description, which depends on the weapon power's type and level.
## Tank Type
- There are three tank types: Speed, Power, and Tactical.
- A loadout has exactly one tank type.
- A tank type has a tank power. This is fixed per tank type, so this is just a description.
- A tank type determines which gadgets are available to the loadout.
  - Only one gadget is allowed to match a different tank type. For a Speed tank, this is a Tactical gadget. For a Power tank, this is a Speed gadget. For a Tactical tank, this is a Power gadget.
- A tank type determines which relic powers are available to the loadout.
  - Only one relic power is allowed to match a different tank type. For a Speed tank, this is a Tactical relic power. For a Power tank, this is a Speed relic power. For a Tactical tank, this is a Power relic power.
  - Some relic powers do not have a type and therefore are available to all tank types.
## Gadget
- A loadout has zero through three gadgets.
- Each gadget has a type that matches one of the tank types.
- A gadget contains gadget part options, which can be selected to equip the part to the gadget.
- All gadgets have the same number of gadget part slots, determined by the player's progression.
- A gadget part can be equipped if all the following conditions are met:
  - The total cost of the equipped gadget parts will not exceed the number of gadget part slots.
  - The total number of equipped gadget parts will not exceed nine.
- A gadget may not have more than one gadget part with the same effect equipped at a time.
  - Attempting to equip a gadget part with the same effect will remove the existing one.
## Gadget Part
- A gadget part is associated with a specific gadget.
  - Two gadget parts belonging to different gadgets are distinct entities, even if they have identical attributes.
- A gadget part has a type, rarity, cost, and value.
- A gadget part's rarity ranges from one through five.
- A gadget part's cost ranges from one through ten.
- A gadget part has a description that depends on the type.
- A gadget part's value describes the strength of the gadget part's effect mentioned in the description.
  - Depending on the effect, the value can be a string (such as "Large", "2 times", or "ON"), a percentage (such as "20%"), or an integer (such as "2")
- A gadget part can be upgraded.
  - An upgraded gadget part's cost is reduced by zero through two, depending on the part.
  - An upgraded gadget part contributes a percentage damage buff to the gadget, depending on the part.
## Relic Power
- A loadout has zero through five relic powers.
- A relic power has a type, a level, and optionally a type that matches one of the tank types.
- A relic power's level ranges from one through three.
- A relic power has a description that depends on the type and level.
## Loadout Visibility
- A loadout is either public or private.
- Public loadouts may be viewed by any user.
- Public loadouts may be directly accessed through a URL.
- Private loadouts may only be viewed by their owner.
# Non-functional Requirements
## Cost
- During normal expected usage, production infrastructure should cost no more than $25/month.
- During an unusually high-traffic period, such as following a major game update, production should cost no more than $100/month.
- Development and testing infrastructure should be minimized when not in use.
- TODO: Formally define "normal expected usage" and "high-traffic period".
  - Tentatively: Normal usage is 10,000 monthly active users and 200,000 API requests per month.
  - Tentatively: High usage is 100,000 monthly active users and 2,000,000 API requests per month.
## Performance
- The application should provide responsive interactions under normal expected load.
- API requests for common operations should normally complete within an agreed latency target.
- Public loadout pages should load efficiently.
- TODO: Add missing requirements (if any) and define target values.
## Availability
- The application should remain available without manual scaling during normal usage.
- A failure of an individual request should not cause the entire application to become unavailable.
- The system should provide appropriate error responses when dependent services are unavailable.
- TODO: Define the number of 9s for availability (SLA).
## Security
- Authentication credentials must not be stored directly by the application.
- Users must only be able to modify the resources that they own.
- Private loadouts must not be exposed to unauthorized users.
- The frontend must not contain long-lived AWS credentials.
- Production communication must use HTTPS.
- User input must be validated before being processed or persisted.
- Production infrastructure should follow the principle of least privilege.
## Maintainability
- The application should have automated tests for important domain and application behavior.
- Production infrastructure should be reproducible from source-controlled infrastructure definitions.
- Application deployments should be automated through CI/CD.
- Configuration should be separated from application code.
- Significant architectural decisions should be documented.
# Scope
## MVP
The initial release will support:
- User registration and authentication
- Creating loadouts
- Editing loadouts
- Deleting loadouts
- Public/private loadouts
- Browsing public loadouts
- Viewing individual public loadouts
- Sharing public loadouts through direct URLs
- Tracking favorite weapons
- Tracking unlocked Gadget Parts
## Out of Scope
The following features are intentionally excluded from the initial release. They are likely to be implemented later, but not guaranteed.
- Loadout import
- Screenshot-based loadout recognition
- Automated build suggestions
- Advanced loadout filtering and search
- Tagging the user's own loadouts to organize them
- Loadout statistics and popularity metrics
- Social features such as reactions and player groups
# Assumptions and Open Questions
## Assumptions
- The initial application will not directly communicate with "Splatoon: Raiders".
- Game data will initially be maintained by the application rather than retrieved from an external game API.
- Users manually configure their loadouts.
- The application will initially support web browsers on desktop and mobile-sized screens.
## Open Questions
- What information should be displayed on a public loadout?
- How should public loadouts be sorted?
- What filtering options should public loadout browsing support?
- How should invalid/outdated loadouts be handled if the game data changes after an update?
- What should happen when a game update changes equipment attributes?
- What workload constitutes "normal" and "unusually high" traffic for the cost requirements?
# Constraints
- The initial version will not directly integrate with the game.
- The production architecture must be serverless.
- The application must support anonymous viewing of public loadouts.
- Authentication is required for persistent user-owned data.
- The application must not expose private loadouts to unauthorized users.
