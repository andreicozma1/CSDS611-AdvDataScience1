**Subject** CSDS 611 final project questions

Good afternoon, Dr. Sgouralis,

I wanted to follow up with a few questions about the final project.

- For this project, should we judge success by how close our estimates are to the exact four rates you used, or by how closely our model fits the observed prey and predator populations?
- If we’re judging success by fit, is there a target sum of squared errors (SSE) we should aim for?

We noticed that all 27 observation times are multiples of 5,000, which makes it possible scale all four rates to add whole cycles between those times, while leaving the predicted populations completely unchanged. For this reason, there isn't one unique solution, but multiple possible solutions that are scaled versions of the original set of rates, and the optimizer may end up converging any one of those, right?

If we’re expected to get as close as possible to the one exact set of rates used to generate the original CSV, then we may need observations at times that aren’t multiples of 5,000 to be able to disambiguate. In that case, could you share a few such observations, or an estimate of how long one full cycle takes at the rates you used?

Otherwise, if we should stick with the current CSV, then should we just report one those several possible solutions, and explain how the sampling times allow for this in the report?

From what I remember, you mentioned in class that you used MATLAB’s `ode45` with the default tolerances. Were all the other solver options left at their defaults as well?

Lastly, I also wanted to ask whether where was any additional noise added to the population values before saving them to the CSV?

Best regards,  
Andrei Cozma