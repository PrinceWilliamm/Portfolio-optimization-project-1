This time small-angle approximation wont be used to get a more accurate result. We will not get into details on everything since its so evil but this method works to get a more accurate numerical answer.

**1. Realistic model with no initial angular velocity**

The equation of motion of a pendulum with no initial velocity is the following:
$$
\theta(t)=2\sin^-1[k \times sn(K(k)-\omega t,k)]
$$
To find the angle at some timestep we need to first calculate the values for k and omega
$$
	k=\sin\left( \frac{\theta_{0}}{2} \right)
$$
k is the elliptic modulus
$$
	\omega=\sqrt{ \frac{g}{l} }
$$
omega is the angular frequency and g is the acceleration due to gravity

Next step is to numerically solve the complete elliptic integral of the first kind using a table or software
$$
	K(k)
$$
Then we can finally approach the equation of motion. We first compute the argument of the Jacobi elliptic function sn. 
$$
	\theta(t)=2\sin^-1[k \times sn(K(k)-\omega t,k)]
$$
$$
	u=K(k)-\omega t
$$
$$
	\theta(t)=2\sin^-1[k \times sn(u,k)]
$$
Then compute the Jacobi elliptic function and multiply by k
$$
	v=k\times sn(u,k)
$$
$$
	\theta(t)=2\sin^-1[v]
$$
The answer is in radians.

Now lets see it in practice with some initial conditions. 
$$
	t=0.50s
$$
$$
	\theta_{0}=\frac{\pi}{3}rad
$$
$$
	l=40cm=0.40m
$$
$$
	\dot{\theta}_{0}=0
$$
$$
	k=\sin\left( \frac{\theta_{0}}{2} \right)=\sin\left( \frac{\frac{\pi}{3}}{2} \right)=0.5
$$
$$
	\omega=\sqrt{ \frac{g}{l} }=\sqrt{ \frac{9.81}{0.40} }=4.952272206
$$
Using an online table we find that:
$$
	K(k)=1.6857503548126
$$

$$
	u=K(k)-\omega t
$$
Plugging in the numbers to the expression gives:
$$
	1.6857503548126-4.952272206(0.50)=-0.7903857482
$$
$$
	k\times sn(-0.7903857482)=0.5(-0.6978)=0.3489
$$
$$
	2\sin^-1(0.3489)=-0.7127941755rad
$$
$$
\theta(0.5s)=-0.7127941755rad
$$


Using the small angle approximation would give:
$$
	\theta(0.5s)=\frac{\pi}{3}\cos(\omega t)=-0.8237622294rad
$$
**2. Realistic model with initial angular velocity**
