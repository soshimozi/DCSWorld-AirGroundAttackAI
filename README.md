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
  <tr>
    <td>
      <p>Target</p>
      <p>-Option 1</p>
      <p>-Option 2</p>
      <p>-Option 3</p>
      <p>-Option 4</p>
    </td>
    <td>
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
    <p>Attack with gun</p>
    <p>Attack with unguided rockets</p>
    <p>Attack with unguided bombs</p>
    <p>Attack with guided bombs</p>
    <p>Attack with guided missiles</p>
    <p>Alternatively, the internal DCS code for certain weapon types or combinations of weapon types may be entered as a number</p>
   </td>
 </tr>
 <tr>
  <td>
   <p>ExpendQty</p>
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
   <p>"One"</p>
   <p>"Two"</p>
   <p>"Four"</p>
   <p>"Quarter"</p>
   <p>"Half"</p>
   <p>"All"</p>
  </td>
  <td>
   <p>Number of weapons to be expended per attack run</p>
   <p>Automatic selection of number of weapons to be expended</p>
   <p>Expend one weapon</p>
   <p>Expend two weapons</p>
   <p>Expend four weapons</p>
   <p>Expend 1/4 of weapons carried per type</p>
   <p>Expend 1/2 of weapons carried per type</p>
   <p>Expend all weapons carried per type</p>
  </td>
 </tr>
 <tr>
  <td>
   <p>Dive</p>
   <p>-Option 1</p>
   <p>-Option 2</p>
   <p>-Option 3</p>
  </td>
  <td>
   <p> &nbsp; </p>
   <p>true</p>
   <p>false</p>
   <p>nil</p>
  </td>
  <td>
   <p>Whether a dive attack is performed</p>
   <p>Perform a dive attack (when possible)</p>
   <p>Perform a level attack (when possible)</p>
   <p>Perform a level attack (when possible)</p>   
  </td>
 </tr>
 <tr>
  <td>
   <p>OffsetAngle</p>
   <p>-Option 1</p>
   <p>-Option 2</p>
   <p>-Option 3</p>   
  </td>
  <td>
   <p> &nbsp; </p>
   <p>number</p>
   <p>0</p>
   <p>nil</p>
  </td>
  <td>
   <p>Offset turn to side prior to pop-up maneuver</p>
   <p>Angle in degrees of offset turn (enter positive number only, offset side is determined by egress geometry)</p>
   <p>Do not perform an offset turn</p>
   <p>Do not perform an offset turn</p>   
  </td>
 </tr>
 <tr>
  <td>ClimbAngle</td>
  <td>number</td>
  <td>The climb angle in degrees for any pop-up climb (climb angles smaller than 15 are not possible)</td>
 </tr>
 <tr>
  <td>
   <p>PopAlt</p>
   <p>-Option 1</p>
   <p>-Option 2</p>
   <p>-Option 3</p>   
  </td>
  <td>
   <p> &nbsp;</p>
   <p>number</p>
   <p>nil</p>
   <p>nil</p>   
  </td>
  <td>
   <p>Pop-up maneuver prior to attack</p>
   <p>Height in meters above target to which a pop-up shall be performed</p>
   <p>Do not perform a pop-up maneuver</p>
   <p>Do not perform a pop-up maneuver</p>   
  </td>
 </tr>
 <tr>
  <td>
   <p>AttackDist</p>
   <p>-Option 1</p>
   <p>-Option 2</p>
   <p>-Option 3</p>   
  </td>
  <td>
   <p> &nbsp;</p>
   <p>number</p>
   <p>nil</p>
   <p>nil</p>   
  </td>
  <td>
<p>Distance from target where a pop-up maneuver shall be completed (if no pop-up maneuver is performed, this is ignored and attacks will be initiated immediately)</p>
<p>Distance in meters (useful to set a specific distance for weapons with stand-off range such as missiles and heavy rockets)</p>
<p>When attacking with bombs, the distance will be calculated automatically in order to keep to pop-up as short as possible</p>
<p>When attacking with rockets, a generic distance is selected automatically that works with the most common rocket types</p>   
  </td>
 </tr>
 <tr>
  <td>
   <p>Reattack</p>
   <p>-Option 1</p>
   <p>-Option 2</p>
   <p>-Option 3</p>   
  </td>
  <td>
   <p> &nbsp; </p>
   <p>true</p>
   <p>false</p>
   <p>nil</p>   
  </td>
  <td>
   <p>Whether aircraft egress after the first attack or return for subsequent attacks</p>
   <p>Repeat attacks as long as weapons and targets remain</p>
   <p>Egress after first attack</p>
   <p>Egress after first attack</p>   
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
