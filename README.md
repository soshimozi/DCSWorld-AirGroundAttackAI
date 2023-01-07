# DCSWorld-AirGroundAttackAI

<a href="https://www.youtube.com/embed/n4VBS7AQJFk?feature=oembed" target="_blank"><img src="https://i3.ytimg.com/vi/n4VBS7AQJFk/maxresdefault.jpg" 
alt="Single Player Missions"/></a>
(all scenes show a single AI-flight)

##### Features:

* Realistic offset pop-up attacks from low level which have not previously been possible using default DCS AI behavior. This allows AI aircraft to approach targets at low level in cover from high/medium range SAMs, then pop-up to attack from above the AAA threat, thus greatly increasing AI survivability in high-threat environments.
* Ability to set-up various traditional level and dive attack profiles.
* Depending on ingress-egress geometry, aircraft in a flight can perform offset pop-up attacks from one or two sides.
* Each aircraft is able to attack its own sub-target element independently, allowing simultaneous attacks of all aircraft in a flight against multiple vehicles, ships, static objects or scenery objects. With default DCS AI behavior this has not been possible for static or scenery objects.
* After weapons release, all aircraft in a flight will perform a hard turn towards the egress direction and proceed towards the egress point individually, where the flight will form up again. This eliminates standard DCS AI behavior where flights will try to reform directly after weapon release, leading to unnecessary maneuvering in the target area. This also means that all aircraft are free to immediately climb/descend back to safe altitude after weapon release (default DCS AI behavior means that the flight leader is unable to change altitude until all wingmen have rejoined, leading to lingering at weapon release altitude over the target area).
* Works for full AI flights and for AI wingmen of human players.
 

##### Mission Editor Instructions:

* Include the “AirGroundAttackScript.lua” with a "Do Script File" trigger in your mission.
* At the waypoint where you want your flight start the attack, under Advanced Waypoint Actions, add a Run Script action. Insert the following code to this action:
```lua 
AirGroundAttackTask(FlightName, Target, WeaponType, ExpendQty, Dive, OffsetAngle, ClimbAngle, PopAlt, AttackDist, Reattack)
```



<table cellpadding="1" cellspacing="1" border="1">
  <tr><th>Flight Name</th><th>"Aerial-1"</th><th>Group name of flight that is tasked to attack</th>
  <tr valign="center">
    <td width="12%">
      <p>Target</p>
      <p>-Option 1</p>
      <p>-Option 2</p>
      <p>-Option 3</p>
      <p>-Option 4</p>
    </td>
    <td width="30%">
      <p> &nbsp; </p>
      <p>"Ground-1"</p>
      <p>{"StaticName-1", "StaticName-2", "StaticName-N"}</p>
      <p>{{x = 123, y = 123},{x = 456, y = 456}}</p>
      <p>{x = 123, y=123}</p>
    </td>
    <td>
     <p>Four types of ground targets can be attacked (vehicles/ships, static objects, scenery objects, parked aircraft/helicopters)</p>
     <p>Vehicles/Ships: Group name of vehicle or ship group</p>
     <p>Static Objects: Object name of static object, listed in {} (a single static objects also needs {} ).</p>
     <p>Scenery Objects: x-/y-coordinate of scenery object in {}, listed in {} (a single scenery objects needs double {{}} ).</p>
     <p>Parked aircraft or helicopters: x-/y-coordinate in {}. Stationary aircraft or helicopters within 5000 m of this coordinate will be attacked.</p>
    </td>
  </tr>
  <tr>
   <td>
    <p>WeaponType</p>
    <p>-Option 1</p>
    <p>-Option 2</p>
    <p>-Option 3</p>
    <p>-Option 4</p>
    <p>-Option 5</p>
    <p>-Option 6</p>
    <p>-Option 7</p>
   </td>
  <td>
   <p> &nbsp; </p>
   <p>"Auto"</p>
   <p>"Cannon"</p>
   <p>"Rockets"</p>
   <p>"Bombs"</p>
   <p>"Guided bombs"</p>
   <p>"ASM"</p>
   <p>number<p>
  </td>
   <td>
    <p>Weapon type for the attack</p>
    <p>Automatic weapon type selection (note: might lead to gun strafing)</p>
   </td>
 </tr>
</table>

Notes and known issues:

* The offset pop-up attacks have been scripted to be as realistic and smooth as possible. You will note that when attacking with bombs, after climbing and rolling into the target, AI aircraft will fly level for 10+ seconds before starting to dive. This unfortunately is due to the way the DCS AI is set up and is unavoidable, as the AI needs a certain distance from the target to attack it. This level flight part has carefully been scripted to be as short as possible for any given speed and altitude (if it is made too short, the AI will turn around and return from a longer distance). You will notice that when attacking with rockets, the AI is able to dive on the target instantly.
* Offset side for a pop-up attack is automatically selected based on egress direction. If the egress waypoint is in the right quarter of the target, aircraft will offset left and attack towards the right (and vice versa). If the egress direction is either in the quarter ahead or behind of the target (from where the flight came from), the flight will split and make a pincer attack from left and right simultaneously.
* The next waypoint after the attack waypoint (where the attack is tasked) is automatically selected as the egress waypoint. Alternatively, if any waypoint is named “Egress”, it will be selected as egress waypoint instead (this way you can have the attack waypoint ahead of the target, a waypoint at the target itself and the next waypoint named “Egress” away from the target).
* Aircraft in a flight will slightly modulate offset angle, climb angle and pop-up altitude in order to create timing separation over the target.
* The script also works for AI wingman of a human player. Set up the task for the player flight in the Mission Editor exactly the same as for an AI flight. During the mission, before reaching the attack waypoint, order “Attack Mission Target and Rejoin” via the radio. Your AI wingmen will perform their attacks as set-up, proceed to the egress point and then form up with you again without any further commands required.
* I made a very big effort to accurately calculate the maneuver geometry for pop-up attacks. As the execution of this maneuvers by the AI is highly depending on many factors (such as aircraft type, speed, altitude, weight, AOA, available Gs, turn radius as well as some DCS bugs), there might be cases where the AI will not be in the anticipated position when rolling out on the target and not initiate an attack. Hopefully it will be rare, but better first verify that any combination of aircraft type, weapons, offset angle, climb angle, pop-up altitude etc. works correctly.
* Offset pop-up attacks over uneven terrain might be problematic. There seems to be a DCS bug that minimum attack distance is depending on aircraft height above terrain below the aircraft, instead of aircraft height above the target. This means that pop-up maneuvers may fail to lead to the AI initiating an attack if they are over higher terrain than the target elevation at that moment. Higher targets (such as on a hilltop) with pop-ups over lower ground are not affected by this problem. The attack geometry is actually always calculated correctly and takes target elevation into account.
