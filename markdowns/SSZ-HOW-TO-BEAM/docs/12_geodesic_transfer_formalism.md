# Geodesic Transfer Formalism

Canonical static spherical SSZ metric:

\[
ds^2=-D(r)^2c^2dt^2+D(r)^{-2}dr^2+r^2d\Omega^2
\]

with

\[
D(r)=\frac{1}{1+\Xi(r)}.
\]

For a timelike test particle:

\[
E=D(r)^2c^2\frac{dt}{d\tau},\quad L=r^2\frac{d\phi}{d\tau}
\]

and

\[
\left(\frac{dr}{d\tau}\right)^2=\frac{E^2}{c^2}-D(r)^2\left(c^2+\frac{L^2}{r^2}\right).
\]

BEAM-SSZ v0.4 uses these equations to replace the older worldline-only proxy with geodesic consistency checks.
