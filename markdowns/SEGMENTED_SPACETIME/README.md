# SEGMENTED_SPACETIME

# Exponential Triangle – Gravitation vs. Segmented Spacetime

This interactive visualization explores the relationship between gravitational intensity (λ), segment count (N), and the deformation of space and time.

A single HTML file demonstrates how λ affects both spatial and temporal geometry using simple triangular representations and exponential growth.

## 🚀 What It Shows

- The upper triangle visualizes **space deformation** (r(N)).
- The lower triangle represents the **time required** to traverse that deformed space (r(t)).
- A slider lets you adjust λ (gravitational factor).
- N is automatically derived from λ using a logistic approximation.
- The exponential function applies:

![image](https://github.com/user-attachments/assets/00de6b04-8ae0-42eb-ac4c-bfab6aead789)


## 🧠 What's the Idea?

The visualization is based on the assumption that space is **not continuous**, but **segmented**.

> Stronger gravitation → More segmentation → Greater temporal cost to cross the same space.

This model challenges the flat, Newtonian space-time intuition and leans into visual relativity.

## 🔍 What Do x, y and z Represent?

In the **upper triangle**:
- Point **x**: starting point in space
- Point **y**: destination along the y-axis (defined by λN)
- Line **x–y**: the real **path** through segmented space

In the **lower triangle**:
- Point **z**: target point in time
- Line **x–z**: the **temporal cost** to reach from x to y

So we have:
- **λN = y** → vertical displacement from gravitation
- **x–y = spatial path**
- **x–z = time needed**

The higher the λ, the more segmented the space becomes → the longer the journey → the more time it takes.

## 📦 Files Included

- `Slider.html`: Main visualization with interactive slider
- `README.md`: This file

## 🧪 Formula Detail

- Segment count (logistic):  

![image](https://github.com/user-attachments/assets/f70471b4-c77f-44f3-a7ca-d18e4d1d7e53)

- Space deformation:  
![image](https://github.com/user-attachments/assets/b26c6d7d-9523-4ac5-805d-16acc218e80d)


---


λN is y.

x to y is the spatial path.

x to z is the temporal path.

If λ increases, then N increases as well. 
Because N is not a free parameter.
Gravitation (λ) segments space (N).

More segments = more time needed to cross the same space.

This is visualized here using exponential stretching of the triangles.

r(N) = r₀ * e^(λN)

https://error-wtf.github.io/SEGMENTED_SPACETIME/Slider.html

## License

*ANTI-CAPITALIST SOFTWARE LICENSE (v 1.4)* 2025 © Carmen Wrede and Lino Casu


