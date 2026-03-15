# Circadian Sleep Optimization

Hello,
  
In this project I will be trying to calculate an optimal sleeping time depending on the location and the time. 

For this we will be calculating the sunrise and sunset.

$$
$$

Sunrise happens when the Sun's center reaches the horizon.

Astronomically that means:

$$
Sun\space altitude = -0.833\degree
$$

The -0.833 $\degree$ correction exist because:
- The sun has a radius $0.5\degree$
- The atmosphere bends light upward (refraction = $0.33\degree$)

The altitude of the Sun above the horizon is given by:

$$
sin(h) = sin(\phi)sin(\delta) + cos(\phi)cos(\delta)cos(H)
$$

Where:
- h = Sun altitude
- $\phi = Latitude$
- $\delta = Solar\space declination$
- H = Hour angle

At sunrise h = -0.833 $\degree$

Plugging it in:

$$
sin(-0.833\degree) = sin(\phi)sin(\delta) + cos(\phi)cos(\delta)cos(H)
$$

Now we solve for H.

$$
H = arccos(\space\frac{sin(-0.833\degree) - sin(\phi)sin(\delta)}{cos(\phi)cos(\delta)}\space)
$$

Two parameters must be known in order to apply the formula,
- $\delta = Solar\space declination$
- $\phi = Latitude$

To calculate the solar declination we use this formula:

$$
\delta = 0.006918−0.399912cos(\gamma)+0.070257sin(\gamma)−0.006758cos(2\gamma)+0.000907sin(2\gamma)−0.002697cos(3\gamma)+0.00148sin(3\gamma)
$$

Where $$\gamma$$ is the fractional year.

Fractional year($\gamma$) tells us how many radians we have moved after the first day of the year.

$$
\gamma = \frac{2\pi}{365}(N-1)
$$

Where N is the day of the year (1-365)

$$
$$

To find the latitude we will ask the user to input their location from the map that pops up on their screen.

$$
$$

Following this we should first convert the hour angle to time and then find the solar noon and find our sunset and sunrise times. 

$$
$$

The hour angle H represents how far the Earth must rotate from solar noon until the Sun reaches the horizon.
Since the Earth rotates:

$$
360\degree = 24 \space hours
$$

we obtain:

$$
1\degree = 4 \space minutes
$$

Therefore: 

$$
H_{minutes} = \frac{H \cdot 180}{\pi}\space \space x \space 4
$$

This gives us the time difference between solar noon and sunrise/sunset.

The final step is to calculate solar noon.
Solar noon is the moment when Sun reaches its highest point in the sky.

However, solar noon is not always exactly 12:00 because of:
- the tilt of Earth's axis
- the elliptical shape of Earth's orbit
The difference is corrected using the Equation of Time.
The equation of time is given by:

$$
E = 229.18(0.000075+0.001868cos(\gamma)−0.032077sin(\gamma)−0.014615cos(2\gamma)−0.040849sin(2\gamma))
$$

Where E is measured in minutes.

Using this correction we compute the solar noon:

$$
Solar \space Noon = 720 - 4\lambda - E + timezone
$$

Where:
- 720 represents 12:00 in minutes
- $\lambda$ is the longitude of the location (in degrees)
- E is the equation of time correction
- timezone is the local timezone offset in minutes

The result is expressed as the number of minutes after midnight.
This value can then be converted into standard clock time.

Once we know solar noon and the hour angle, we can compute the sunset and sunrise times.

$$
Sunrise = Solar \space Noon - H_{minutes}
$$

$$
Sunset = Solar \space Noon + H_{minutes}
$$

This provides the time of sunrise and sunset for a given:
- location 
- date

Workflow:
1. User selects location on map

2. Latitude and longitude are extracted
        
3. The current date is converted to day of year (N)
        
4. Fractional year (γ) is calculated

5. Solar declination (δ) is computed

6. Hour angle (H) is calculated

7. Solar noon is computed

8. Sunrise and sunset times are obtained


These values will later be used to determine the optimal sleeping schedule based on the natural light–dark cycle.
