### Starting with basic complex calculations; ###
$$𝑧_1 = 1 + 𝑖, 𝑧_2 = 1 + 3𝑖$$
Therefore
$$z_1 * z_2 = 1+4i$$
and, 
$$\frac{z_1}{z_2}=\frac{1+i}{1+3i} \times \frac{1-3i}{1-3i} = \frac{(1+i)(1-3i)}{(1+3i)(1-3i)}$$ By using the formula $(a+bi)(a-bi) = a^2 + b^2$ we can find that the denominator expands to;
$$(1+3i)(1-3i) = 1^2 - (3i)^2 = 1 - 9(i^2)$$
Since $i^2 = -1$:
$$1 - 9(-1) = 1 + 9 = 10$$
And the numerator expands to;
$$(1+i)(1-3i) = 1(1) + 1(-3i) + i(1) + i(-3i)$$
$$= 1 - 3i + i - 3i^2$$
Substitute $i^2 = -1$:
$$= 1 - 2i - 3(-1)$$
$$= 1 - 2i + 3 = 4 - 2i$$
Combining these two, we achieve the answer
$$\frac{4 - 2i}{10} = \frac{4}{10} - \frac{2}{10}i$$
Reduce the fractions to lowest terms:
$$\frac{2}{5} - \frac{1}{5}i \quad$$
### Moving into more evil ones ###
When exponenting complex numbers the general formula comes handy;
$$z_1^{z_2} = e^{z_2 \ln(z_1)}$$
Writing $z_1$ into polar form
	To compute $\ln(z_1)$, we need its magnitude $r$ and principal argument $\theta$:
**Magnitude ($r$):**
    $$\vert{}z_1\vert{} = \sqrt{1^2 + 1^2} = \sqrt{2}$$
**Argument ($\theta$):**$$\theta = \arg(z_1) = \arctan\left(\frac{1}{1}\right) = \frac{\pi}{4}$$So $z_1$ in exponential form is:

$$z_1 = \sqrt{2} e^{i \frac{\pi}{4}}$$
Using principal branch of the complex logarithm $\ln(z) = \ln\vert{}z\vert{} + i \arg(z)$:
$$\ln(1+i) = \ln(\sqrt{2}) + i \frac{\pi}{4} = \frac{1}{2}\ln(2) + i \frac{\pi}{4}$$
Furhtermore multiplying $z_1 with z_2$:
$$z_2 \ln(z_1) = (1 + 3i) \left( \frac{1}{2}\ln(2) + i \frac{\pi}{4} \right)$$
Expanding towards the correct solution
$$= 1 \cdot \left(\frac{1}{2}\ln(2)\right) + 1 \cdot \left(i \frac{\pi}{4}\right) + 3i \cdot \left(\frac{1}{2}\ln(2)\right) + 3i \cdot \left(i \frac{\pi}{4}\right)$$

$$= \frac{1}{2}\ln(2) + i \frac{\pi}{4} + i \frac{3}{2}\ln(2) + 3i^2 \frac{\pi}{4}$$
Using Euler's formula $e^{a + bi} = e^a (\cos \theta + i \sin \theta)$ to find the final polar form
$$z_1^{z_2} = e^{\left(\frac{1}{2}\ln(2) - \frac{3\pi}{4}\right)} \cdot e^{i \left(\frac{\pi}{4} + \frac{3}{2}\ln(2)\right)}$$

## Complex Daniel equation ##
Some evil rule
$$\int_C \frac{1}{z} \, dz = 0$$Find the points where the integrand $f(z) = \frac{1}{z^2 + 1}$ is not analytic by setting the denominator equal to zero:

$$z^2 + 1 = 0 \implies z^2 = -1 \implies z = \pm i$$

Factor the denominator:

$$f(z) = \frac{1}{(z - i)(z + i)}$$

Both $z_1 = i$ and $z_2 = -i$ are **simple poles** (poles of order 1).

### Step 2: Calculate the Residue at $z = i$

Use the residue formula for a simple pole $\text{Res}(f, z_0) = \lim_{z \to z_0} (z - z_0) f(z)$:

$$\text{Res}(f, i) = \lim_{z \to i} (z - i) \frac{1}{(z - i)(z + i)} = \lim_{z \to i} \frac{1}{z + i}$$

Substitute $z = i$:

$$\text{Res}(f, i) = \frac{1}{i + i} = \frac{1}{2i} = -\frac{i}{2}$$

### Step 3: Calculate the Residue at $z = -i$

$$\text{Res}(f, -i) = \lim_{z \to -i} (z - (-i)) \frac{1}{(z - i)(z + i)} = \lim_{z \to -i} \frac{1}{z - i}$$

Substitute $z = -i$:

$$\text{Res}(f, -i) = \frac{1}{-i - i} = \frac{1}{-2i} = \frac{i}{2}$$

### Step 4: Apply the Cauchy Residue Theorem

The Residue Theorem states:

$$\oint_C f(z) \, dz = 2\pi i \sum \text{Res}(f, z_k)$$

Sum the residues:

$$\sum \text{Res} = \text{Res}(f, i) + \text{Res}(f, -i) = \frac{1}{2i} + \left(-\frac{1}{2i}\right) = 0$$

Substitute back into the integral formula:

$$\oint_C \frac{1}{z^2 + 1} \, dz = 2\pi i (0) = 0$$

### Final Answers by Contour Choice

- **If $C$ encloses both poles $z = \pm i$** (e.g., $\vert{}z\vert{} = 2$):
    
    $$\oint_C \frac{1}{z^2 + 1} \, dz = 0$$
    
- **If $C$ encloses only $z = i$** (e.g., upper half-plane contour):
    
    $$\oint_C \frac{1}{z^2 + 1} \, dz = 2\pi i \left(\frac{1}{2i}\right) = \pi$$

## Second complex daniel väsäys ##

$$I = \oint_C \frac{e^z}{z^2 + 4} \, dz$$
Further calculating
$$z^2 + 4 = 0 \implies z^2 = -4 \implies z = \pm 2i$$

Factor the denominator:

$$f(z) = \frac{e^z}{(z - 2i)(z + 2i)}$$

Both $z_1 = 2i$ and $z_2 = -2i$ are **simple poles** (poles of order 1).

### Step 2: Calculate the Residue at $z = 2i$

Using the simple pole residue formula $\text{Res}(f, z_0) = \lim_{z \to z_0} (z - z_0) f(z)$:

$$\text{Res}(f, 2i) = \lim_{z \to 2i} (z - 2i) \frac{e^z}{(z - 2i)(z + 2i)} = \lim_{z \to 2i} \frac{e^z}{z + 2i}$$

Substitute $z = 2i$:

$$\text{Res}(f, 2i) = \frac{e^{2i}}{2i + 2i} = \frac{e^{2i}}{4i}$$

### Step 3: Calculate the Residue at $z = -2i$

$$\text{Res}(f, -2i) = \lim_{z \to -2i} (z - (-2i)) \frac{e^z}{(z - 2i)(z + 2i)} = \lim_{z \to -2i} \frac{e^z}{z - 2i}$$

Substitute $z = -2i$:

$$\text{Res}(f, -2i) = \frac{e^{-2i}}{-2i - 2i} = \frac{e^{-2i}}{-4i} = -\frac{e^{-2i}}{4i}$$

### Step 4: Apply the Cauchy Residue Theorem

The Residue Theorem states:

$$\oint_C f(z) \, dz = 2\pi i \sum \text{Res}(f, z_k)$$

Sum the two residues:

$$\sum \text{Res} = \text{Res}(f, 2i) + \text{Res}(f, -2i) = \frac{e^{2i}}{4i} - \frac{e^{-2i}}{4i} = \frac{e^{2i} - e^{-2i}}{4i}$$

Using Euler's identity for sine, $\sin(\theta) = \frac{e^{i\theta} - e^{-i\theta}}{2i}$:

$$\sum \text{Res} = \frac{1}{2} \left( \frac{e^{2i} - e^{-2i}}{2i} \right) = \frac{1}{2} \sin(2)$$

Substitute this sum back into the Residue Theorem:

$$I = 2\pi i \left( \frac{1}{2} \sin(2) \right) = \pi i \sin(2)$$

### Final Answers by Contour Choice

- **If $C$ encloses both poles $z = \pm 2i$** (e.g., circle $\vert{}z\vert{} = 3$):
    
    $$\oint_C \frac{e^z}{z^2 + 4} \, dz = \pi i \sin(2)$$
    
- **If $C$ encloses only $z = 2i$** (e.g., upper half-plane contour):
    
    $$\oint_C \frac{e^z}{z^2 + 4} \, dz = 2\pi i \left( \frac{e^{2i}}{4i} \right) = \frac{\pi e^{2i}}{2}$$