# Epitech TV front-end

This is the front end to the Epitech Strasbourg TV system. It is a modular web
display which shows informations relevant to Epitech Strasbourg students such as
the time of day, the room reservations and the remaining time until the next
Star Wars movie is released.

This web viewer utilizes a proxy back end in order to perform API calls.

## Modules

| Module           | Status  |
| ---              | ---     |
| Line layout      | Done    |
| Card layout      | Done    |
| Slideshow layout | Planned |
| Clock            | Done    |
| Calendar         | Done    |
| Top view         | Done    |
| Twitter          | WIP     |
| Countdown        | WIP     |
| Weather          | Planned |
| News             | Planned |
| Video            | Planned |

## Components

This web display uses the Polymer framework in order to provide a markup with a
simple structure which directly reflects the desired layout. Hence several
Polymer components are defined by this application.

### Layout components

The `vertical-layout` and `horizontal-layout` components do exactly as implied
and arrange child components in a vertical or horizontal way. This is done
using flexboxes.

> TODO: Merge `vertical-layout` and `horizontal-layout` into a `linear-layout`
> which would use a `horizontal` or `vertical` property.

The `card-layout` displays all child elements onto a material design card.

### Clock data component

The `clock-data` component does not render anything and, in fact, does not have
any markup to it. You can find examples of its uses in the `clock-digital`, `clock-countdown` or `room-planning` components.

#### Input properties

`interval` : The interval between each "tick" as an ISO 8601 duration ;
defaults to `P0Y0M0DT0H0M1S` ( one second ).

`offset` : The offset of each "tick" as an ISO 8601 duration ; defaults to
`P0Y0M0DT0H0M0S` ( zero seconds ).

`autoStart` : Whether the timer should automatically start ticking as soon as
it is ready.

#### Output properties

`current` : The current "tick" as an ISO 8601 date.

`next` : The next "tick" as an ISO 8601 date.

#### Methods

`start()` : Starts the timer if it isn't already. Does nothing instead. Returns
nothing.

`stop()` : Stops the timer if it isn't already. Does nothing instead. Returns
nothing.

#### Events

The `tick` event is fired at each "tick". Its payload is an object of the
following structure :

``` json
{
	"time": "<ISO 8601 date of the tick>",
	"next": "<ISO 8601 date of the next tick>"
}
```

### Digital clock

The `clock-digital` is a simple ( non-configurable ) digital clock.

### Countdown clock

The `clock-countdown` is a simple countdown clock. Its end is defined with the
`end` property as an ISO 8601 date. Its title is to be inserted as a child `h1`
element.

### Room planning data

The `room-data` component retrieves data from the room planning API. It serves
data concerning the time and date of room reservations.

#### Input properties

`period-start` : the ISO 8601 representation of the earlier bound of the
queried period.

`period-end` : the ISO 8601 representation of the later bound of the queried
period.

`rooms` : the array of room names to be queried.

`refresh-rate` : the rate at which data will be automatically refreshed, in
seconds. A zero value means no refresh.

#### Output properties

`data` : the data object ; each index is a querried room and contains an array
of events.

`error` : `true` if the last request resulted in an error.

### Room planning

The `room-planning` is a column representation of the schedule for room
reservations. Blue events represent EPITECH reservations whereas red events are
ISEG reservations.

#### Input properties

`rooms` : An array containing the names of rooms to be shown at all time ;
defaults to `[]`.

`backup-rooms` : An array containing the names of rooms to be shown whenever it
has an event which matches a tag in `backupTags` ; defaults to `[]`.

`backup-tags` : An array containing tags which will trigger the display of
`backup-rooms` ; defaults to `["sm"]`.

`default-start-of-day` : The default earliest time of day to be displayed ;
defaults to `"8:00"`.

`default-end-of-day` : The default latest time of day to be displayed ;
defaults to `"20:00"`.

### Backup rooms

The `room-planning-backup` component either shows a list of rooms having an
event matching a tag within the day, or — if there is no such room — hides
itself.

#### Input properties

`rooms` : An array containing the names of rooms to be shown.

`backup-tags` : The tags to be tested in order to determine whether a room
shall be shown.

### Room planning with backup information

The `room-planning-with-backup` component is a simple composition of
`room-planning` and `room-planning-backup` and each of its properties is
directly mapped to a property of its children.

#### Input properties

`rooms` : Mapped to the `room-planning`'s `rooms` property.

`column-backup-rooms` : Mapped to the `room-planning`'s `backup-rooms` property.

`text-backup-rooms` : Mapped to the `room-planning-backup`'s `rooms` property.

### Room planning plan view

The `room-planning-dome-2` component was specifically built to provide a
graphical view of current room reservations within the second floor of the Dome
building of EPITECH Strasbourg. It uses inline SVG and CSS in order to embed
the plan to the display.
