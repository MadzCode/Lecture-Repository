### working code

```cpp
// 1. Fixed the loop condition in UpdatePositions
for (size_t i = 0; i < entities.size(); ++i)  // Corrected: loop over 'entities'

// 2. Fixed the position updates
entities[i].positionX += entities[i].velocityX * deltaTime;  // Corrected: use += for positionX
entities[i].positionY += entities[i].velocityY * deltaTime;  // Corrected: use += for positionY
entities[i].positionZ += entities[i].velocityZ * deltaTime;  // Corrected: use += for positionZ
```
