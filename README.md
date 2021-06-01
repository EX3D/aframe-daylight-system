# aframe-daylight-system


W.I.P Component. Based on <a href="https://github.com/feiss/aframe-environment-component">aframe-environment-component </a> a simple daylight system with latitude and hour inputs.


![Example Image](https://github.com/EX3D/aframe-daylight-system/blob/main/daylightsystem(1).gif)

Based on aframe-environment-component this component is made for creators that want to set up a particular sun position using, latitude, declination and hour data for a project.

This uses vec3 conversion from sun azimuth and sun altitude equations. 

## WIP

- Implement schema components: Longitude (adds variance to both sun altitude and azimuth. See: https://en.wikipedia.org/wiki/Position_of_the_Sun) ...........done

- Add North Offset.......wip

- Merge light object functionality from aframe-environment-component or convince them to add this kind of input. That would be awesome........wip

- Remake the way it parses timeOfDay and declination values to something like:

```html 
     <a-entity id="env" daylightsystem = "timeOfDay: 10:35am; timeOfYear: June22"></a-entity>
```


### A-Frame entity notation

```html 
     <a-entity id="env" daylightsystem = "timeOfDay: 9.45; declination: -12.45; latitude: -4.8;"></a-entity>
```

### How it works and Why

![Example Image](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Azimuth-Altitude_schematic.svg/330px-Azimuth-Altitude_schematic.svg.png)
*Credit wikimedia commons.

Sun position in the sky of a reference point is measured using 2 types of angles: 

- The Azimuth determines the angle of the sun in the sky fron the North direction: at daylight it will always travel from East to West (from 90° to 180° of  Azimuth).

- The Elevation angle is the <a href="https://en.wikipedia.org/wiki/Angle#Combining_angle_pairs">complementary angle</a> of the Zenith angle. The later determines the position of the sun from the uppermost point in the sky called ZENITH. 


These angles are affected primarily by 3 factors: 

- Time of day will affect the Azimuth angle and Elevation angle. In the morning the sun is placed towards East and in the afternoon towards West. Sun elevation is always higher at noon and always lower at midnight.

- Latitude <a href="https://en.wikipedia.org/wiki/Latitude">is the relative position of the reference point in a spheroid in relation to it's poles</a> : it affects the Azimuth and Elevation. It varies from -90° to +90°. At the equator the latitude will be 0° and so without any other variable the position of the sun will be parallel to the East-West direction. On the contrary at 90° the position of the sun will be perpendicular to the vertical axis.

- Declination describes the <a href="https://en.wikipedia.org/wiki/Season">inclination of the axis of rotation of the spheroid in relation to the orbital plane.</a> Because we still live in this tiny particle of sun dust this value varies from -23.45° to + 23.45°. It affects the Elevation angle and determines the overall lenght of daylight. Positive declination numbers result in a South-leaning sun at equator.


**These are all basic factors that DO NOT account for other variables that affect the sun position such as orbital positions and global altitude.

### Component Schema

| Property | Description | Range | Default Value | Implemented |
| -------- | ----------- | ------------- | ------------| ------------|
| `northDirection` | Offsets the north direction of this system | 0.0 to 360.0 | `0` | No |
| `timeOfDay` | Base 24 hours. | 0.0 to 24.0 | `6` | Yes |
| `latitude` | Positive values are North hemisphere | -90.0 to 90.0 | `0` | Yes |
| `declination` | Positive values are "Winter" | -23.45 to 23.45 | `0` | Yes |

## TESTED ON
A-Frame v1.1.0
