See discussions, stats, and author profiles for this publication at: https://www.researchgate.net/publication/391391108

Addressing the Limitations of Arbitrary Precision Computation A Call for
Collaborative Solutions

Preprint · May 2025

DOI: 10.55277/ResearchHub.qn857wwj.1

CITATIONS
0

1 author:

Lino P Casu

Goethe University Frankfurt

11 PUBLICATIONS   7 CITATIONS   

SEE PROFILE

READS
3

All content following this page was uploaded by Lino P Casu on 02 May 2025.

The user has requested enhancement of the downloaded file.

Addressing the Limitations of Arbitrary Precision Computation 
A Call for Collaborative Solutions 
Lino Casu, Akira (AI) 

This paper highlights the significant challenges faced by researchers attempting to implement 
the Chudnovsky algorithm and other arbitrary precision computations in C++ and Python. 
Despite advances in hardware, existing libraries and scripts are insufficient for modern 
scientific needs, limiting both theoretical mathematics and applied sciences like astrophysics. 
This paper critiques the current state of open-source repositories, such as GitHub, which lack 
fully functional scripts, and identifies the bottlenecks in Python and C++ libraries. A 
collaborative solution is proposed to overcome these limitations and harness the true 
potential of modern computing. 

The Chudnovsky algorithm[1] is a highly efficient and widely recognized method for 
computing π to billions or trillions of digits. Developed with precision in mind, this algorithm 
leverages complex mathematical relationships to rapidly converge on accurate values of π. 
However, translating this theoretical framework into practical computational solutions has 
proven challenging. 

Implementing the Chudnovsky algorithm effectively in programming environments such as 
C++ and Python encounters several roadblocks. These challenges stem largely from: 

Library Limitations: Many existing libraries are not designed to handle the extreme 
precision required for such computations, leading to performance bottlenecks and incomplete 
implementations. 

Resource Management: Arbitrary precision calculations demand significant computational 
resources, including memory and processing power. Efficiently managing these resources is 
crucial but remains a difficult task. 

Scalability Constraints: Most available tools are tailored for smaller-scale applications and 
fail to exploit the full potential of modern hardware capabilities, such as multi-threading and 
high memory availability. 

These limitations are evident in both Python and C++ implementations. In Python, widely 
used libraries such as mpmath and decimal are unable to achieve the theoretically unlimited 
precision needed for extensive calculations without significant degradation in performance. 
Similarly, in C++, dependencies on libraries like GMP and MPFR often introduce memory 
management complexities that hinder their effective use in large-scale computations. 

The issues are further documented in practical terms within our GitHub repository[2]. This 
repository showcases the difficulties encountered when attempting to implement high-
precision algorithms in real-world scenarios. These challenges are not merely technical 
nuisances but pose significant barriers to progress in fields like theoretical mathematics and 
astrophysics, where precision is paramount. 

 
 
 
 
 
Through this paper, we aim to shed light on these challenges and emphasize the importance of 
developing better tools and libraries. By leveraging modern computational resources and 
adopting innovative approaches, we can pave the way for more effective and scalable 
solutions to arbitrary precision computation. 

Issues with Current Implementations 

Despite the potential of modern programming languages and libraries, the implementation of 
high-precision algorithms such as Chudnovsky[1] remains fraught with challenges. These 
issues span incomplete public repositories, limitations in popular Python libraries, and 
dependency complexities in C++ ecosystems. Below, we explore these challenges in detail: 

Incomplete Scripts on GitHub 

A review of publicly available repositories reveals that most scripts for the Chudnovsky 
algorithm in C++ are incomplete or lack proper documentation. For example: 

Omission of Critical Components: Many implementations do not include essential functions 
for efficient computation, such as optimized memory handling or factorial calculations. 

Reliance on Specific Configurations: Some scripts require highly specific setups of libraries 
and compiler configurations, making them inaccessible to the broader scientific community. 

The result is a fragmented ecosystem where researchers must heavily modify or even rewrite 
existing code to achieve their goals. This slows progress, introduces errors, and limits the 
reproducibility of results. 

Limitations in Python Libraries 

Python’s popularity in scientific computation stems from its ease of use and extensive library 
ecosystem. However, its native libraries have inherent constraints that make it challenging to 
perform extremely high-precision calculations: 

mpmath and decimal[4]: These libraries provide extended precision capabilities but are not 
designed for calculations requiring theoretically unlimited digits. For instance: 

import mpmath 
mpmath.mp.dps = 1000  # Set precision to 1000 decimal places 
result = mpmath.mpf(math.factorial(6 * k)) / (math.factorial(3 * k) * 
(math.factorial(k) ** 3)) 

Problem: The math.factorial function in Python is not optimized for extremely large 
values, leading to performance bottlenecks and high memory usage. Additionally, as precision 
increases, the libraries’ performance degrades significantly. 

 
 
 
 
 
Underlying C Modules: Many Python libraries rely on C-based modules to ensure 
compatibility with older hardware. While this approach broadens accessibility, it imposes 
artificial limitations on precision and performance, making it difficult to leverage modern 
computing power. 

These constraints force researchers to resort to inefficient workarounds, further exacerbating 
the challenges of high-precision computation. 

C++ and GMP/MPFR Dependency 

C++ is often the preferred language for high-performance computation due to its control over 
hardware resources. However, the ecosystem presents notable drawbacks: 

MPFR and GMP Libraries: MPFR provides reliable arbitrary precision floating-point 
arithmetic but depends on GMP[4] for its core operations. This dependency chain: 

-  Introduces memory management complexities. 
-  Leads to redundancy in certain operations, increasing resource usage. 

For example: 

#include <gmpxx.h> 

mpf_class result(0, precision);  // GMP object initialized with 
precision 

Memory Management: Despite advances in hardware, these libraries fail to fully utilize 
modern memory capacities. Machines with 64GB or more RAM often encounter bottlenecks 
due to inefficient memory allocation strategies. This limitation constrains the maximum 
achievable digit precision and hampers scalability for large datasets. 

Summary of Challenges 

The issues outlined above highlight systemic inefficiencies across Python and C++ 
implementations. Together, these limitations: 

-  Impede progress in theoretical mathematics and applied sciences by restricting the scope 

and scale of high-precision calculations. 

-  Create a fragmented development environment where researchers must navigate 

incomplete scripts and poorly integrated tools. 

-  Prevent optimal utilization of modern hardware, undermining the potential of cutting-edge 

computing resources. 

 
 
 
 
 
 
 
To address these challenges, the scientific and development communities must prioritize the 
creation of more robust, accessible, and efficient tools for arbitrary precision computation. By 
doing so, we can unlock new possibilities for discovery and innovation across a wide range of 
disciplines. 

The Need for Modernized Libraries 

As the availability of high-performance hardware becomes more widespread, the limitations 
of current computational libraries have become increasingly apparent. Modern systems 
equipped with 32GB DDR4 RAM or more, often available at a low cost, present a significant 
opportunity to rethink the design and capabilities of libraries used for high-precision 
calculations. To fully exploit these resources, it is essential to develop libraries that address 
the following requirements: 

Configurable Precision Limits 

Libraries must allow users to dynamically adjust precision based on available system 
resources. For instance, configurations should enable calculations at varying levels of 
precision without requiring manual adjustments to underlying code or scripts. By providing 
this flexibility, researchers can tailor their computations to match their hardware capabilities, 
avoiding unnecessary resource limitations. 

Elimination of Legacy Constraints 

Many existing libraries retain legacy constraints designed for underpowered systems, limiting 
their ability to scale with modern hardware. These constraints include fixed memory 
allocations, single-threaded processing, and compatibility measures that no longer align with 
contemporary computing environments. Eliminating these outdated elements would create 
more efficient and forward-compatible libraries. 

Optimization of Memory Management 

Efficient memory management is critical for handling massive computations, particularly 
those involving high-precision arithmetic. Modern libraries should leverage dynamic memory 
allocation, multi-threading, and parallel processing to maximize performance on systems with 
abundant RAM. This approach minimizes computational bottlenecks and ensures the 
scalability of calculations. 

 
 
 
 
 
 
Theoretical Mathematics 

In theoretical mathematics, researchers often aim to empirically verify the properties of 
irrational numbers, explore numerical patterns, or uncover new mathematical constants. These 
endeavors demand both high precision and computational performance. However, current 
limitations hinder progress in the following ways: 

Precision vs. Performance Trade-offs: Existing libraries often force researchers to 
compromise between achieving high precision and maintaining reasonable computational 
speeds. This trade-off stifles exploratory research, as the time and resources required for 
large-scale calculations become prohibitive. 

Inadequate Tools for Empirical Validation: The inability to conduct calculations with 
trillions of digits or more restricts the empirical validation of theoretical findings. For 
example, verifying the irrationality or transcendence of specific numbers requires tools 
capable of handling extreme precision without performance degradation. 

By modernizing libraries to address these needs, the field of theoretical mathematics could 
advance more rapidly, enabling researchers to pursue previously unattainable goals. 

Applied Sciences 

Fields such as astrophysics, computational chemistry, and climate modeling rely heavily on 
simulations and models that demand extreme precision. Current libraries, however, often fall 
short in their ability to utilize modern computational power efficiently: 

Gravitational Wave Modeling: Simulations of gravitational waves require calculations with 
minimal error tolerance over billions of iterations. Legacy libraries struggle to handle the 
precision and scale required for such models, limiting the accuracy and scope of research. 

Cosmic Inflation Models: Theoretical studies of cosmic inflation involve high-precision 
computations to test hypotheses about the early universe. Inadequate library support forces 
scientists to implement complex workarounds, diverting time and resources from core 
research. 

Chemical Simulations: Molecular dynamics and quantum chemistry calculations often 
require extreme precision to predict reactions and properties accurately. Current tools impose 
artificial limits that hinder detailed and accurate simulations. 

 
 
 
 
 
 
Future Directions 

To overcome these challenges, the development of modernized libraries should prioritize the 
following: 

Integration with Hardware Acceleration: Leveraging GPUs, TPUs, and multi-core CPUs 
can drastically improve the performance of precision-dependent calculations. 

Scalability: Libraries should be designed to scale seamlessly with hardware improvements, 
ensuring compatibility with future computing architectures. 

Collaborative Development: Open-source initiatives involving the scientific community can 
help identify and address the most critical needs, accelerating the creation of robust and 
versatile tools. 

By addressing these gaps, modernized libraries can unlock the full potential of high-
performance hardware, driving innovation and discovery in both theoretical and applied 
sciences. 

Analysis of Current Scripts and Libraries 

Python: Usage of decimal, mpmath, and numpy 

Python is a popular choice for scientific computations due to its flexibility and extensive 
library ecosystem. For arbitrary precision calculations, libraries such as mpmath, decimal, and 
numpy are frequently employed. However, these libraries, while useful, face inherent 
limitations that restrict their efficiency and scalability in high-precision tasks. 

mpmath and decimal 

The mpmath and decimal libraries are widely used to perform extended precision calculations 
in Python. They provide accessible tools for managing large numbers, but they are not 
optimized for handling theoretically unlimited digit precision. For instance: 

import mpmath 

mpmath.mp.dps = 1000  # Set precision to 1000 decimal places 
M = mpmath.mpf(math.factorial(6 * k)) / (math.factorial(3 * k) * 
(math.factorial(k) ** 3)) 

Problem: While this code sets a high precision level, Python’s native math.factorial 
function is not optimized for handling extremely large values. This leads to significant 
performance bottlenecks and high memory usage, particularly in iterative computations like 
the Chudnovsky algorithm, where factorials and other large intermediate values are repeatedly 
calculated. 

The dependency on Python’s interpreted nature also adds to performance overhead, making 
these libraries unsuitable for tasks requiring trillions of digits. 

 
 
 
 
numpy 

numpy is renowned for its efficiency in handling large data arrays and performing matrix 
operations. However, it is not inherently designed for arbitrary precision calculations. When 
high precision is required, numpy often relies on the decimal library for additional support, as 
shown below: 

import numpy as np 

from decimal import Decimal 

# Perform high-precision calculations using Decimal 
precision = Decimal(1) / Decimal(10**50) 
values = np.array([Decimal(1) / Decimal(3)], dtype=object) 

Problem: The reliance on decimal introduces a performance bottleneck. Operations that 
could otherwise be optimized within numpy are slowed down due to the overhead of managing 
precision through software-based abstractions. This approach also increases memory 
consumption, limiting the library’s scalability for extremely large computations. 

Impacts on Arbitrary Precision Computation 

The limitations of Python libraries for arbitrary precision tasks significantly affect their 
applicability in scenarios requiring extreme accuracy: 

Performance Overhead: The layered abstraction inherent in Python and its libraries causes 
significant slowdowns, particularly for high-precision iterative calculations. This makes 
Python less competitive compared to lower-level languages like C++ for tasks requiring 
trillions of digits. 

Handling Edge Cases: Even with mpmath or decimal, certain edge cases—such as extremely 
large factorials or operations involving minuscule precision adjustments—introduce rounding 
errors or computational inefficiencies that cannot be entirely mitigated. 

Opportunities for Improvement 

To enhance Python’s capabilities in arbitrary precision arithmetic, the following strategies 
could be implemented: 

Optimized Factorial Implementations: Developing more efficient methods for computing 
large factorials within libraries like mpmath could reduce computational overhead. 

Integration of Hardware Support: Leveraging GPU or multi-threading capabilities within 
Python libraries could significantly improve performance for large-scale computations. 

 
 
 
 
 
 
Custom Precision Libraries: Creating Python libraries explicitly designed for arbitrary 
precision, with native support for high-performance operations, could bridge the gap between 
accessibility and efficiency. 

By addressing these issues, Python could become a more viable platform for high-precision 
computational tasks in fields like theoretical mathematics, astrophysics, and computational 
chemistry. 

C++: Dependencies on GMP and MPFR 

C++ scripts often leverage GMP[4] (GNU Multiple Precision Arithmetic[5] Library) and MPFR 
(Multiple Precision Floating-Point Reliable Library) for performing arbitrary precision 
calculations. While these libraries provide powerful tools for high-precision arithmetic, their 
use introduces several challenges that limit their scalability and efficiency in modern 
computational environments. 

Dependency Issues 

One of the primary challenges with using MPFR is its reliance on GMP for core arithmetic 
operations. This interdependency, while robust, introduces complexities in memory 
management and resource allocation. For example: 

#include <gmpxx.h> 

mpf_class result(0, precision);  // GMP object initialized with 
precision 

Problem: The coupling of these libraries creates redundancy in certain operations, which 
increases resource usage. This can lead to potential memory leaks, particularly during 
iterative computations such as those in the Chudnovsky algorithm, where large intermediate 
results need to be stored and manipulated. 

The dependency chain also means that any inefficiencies in GMP are propagated to MPFR-
based computations. This makes debugging and optimization more complex, as issues must 
be addressed at multiple levels of the library stack. 

 
 
 
 
 
 
 
 
 
 
 
Limited Hardware Utilization 

Despite the significant advancements in hardware capabilities, including systems with high 
RAM configurations, many C++ implementations impose artificial limitations to ensure 
compatibility with older machines. For instance: 

size_t ram_mb = 2048;  // Limit available RAM to 2GB 

Problem: These constraints prevent the full utilization of modern systems equipped with 
64GB or more RAM. Such limitations result in inefficient computations, as algorithms are 
forced to operate within an artificially restricted memory space. 

Additionally, the lack of seamless support for multi-threading in these libraries further 
exacerbates inefficiencies. While modern processors offer numerous cores for parallel 
processing, GMP and MPFR primarily operate in a single-threaded context. This 
underutilization of hardware resources significantly hampers the potential performance gains 
from contemporary computing architectures. 

Impacts on Arbitrary Precision Computation 

The limitations imposed by these libraries directly affect the scalability of arbitrary precision 
computations. For instance: 

Chudnovsky Algorithm: This algorithm requires handling factorials and large intermediate 
results. The inefficiencies in memory management and dependency chains can lead to 
bottlenecks, making it challenging to compute π to trillions of digits efficiently. 

Resource Overhead: The memory overhead from redundant operations in GMP and MPFR 
increases exponentially with the precision required, leading to slower computations and 
higher resource consumption. 

Opportunities for Improvement 

To address these challenges, the following strategies could be explored: 

Decoupling Libraries: Developing more modular libraries that do not rely heavily on 
dependencies like GMP could reduce redundancy and improve performance. 

Enhanced Multi-Threading Support: Incorporating robust multi-threading capabilities into 
GMP and MPFR would enable better utilization of modern hardware. 

Dynamic Resource Allocation: Allowing scripts to dynamically adjust memory usage based 
on available hardware would improve scalability and efficiency. 

By addressing these issues, the C++ ecosystem could better support the growing demands of 
high-precision computations in fields like theoretical mathematics and astrophysics. 

 
 
 
 
 
Floating-Point and Rounding Errors 

The Problem with Floating-Point Arithmetic 

Floating-point arithmetic, while fundamental to computational mathematics, is inherently 
prone to rounding errors. This limitation arises from the finite representation of real numbers 
in binary form. Even advanced libraries designed for high precision, such as GMP and MPFR, 
are not immune to these challenges, particularly under extreme precision requirements. The 
following issues illustrate this: 

Finite Precision Representation: Computers adhere to standards like IEEE 754, which 
represent floating-point numbers using a fixed number of bits. This inherently introduces 
approximation errors when storing irrational or extremely large numbers, as these numbers 
cannot be precisely represented in binary. 

Cascading Errors: In iterative calculations, such as those employed by the Chudnovsky 
algorithm, small rounding errors compound over successive iterations. This accumulation can 
lead to significant deviations from the true result, compromising the accuracy of high-
precision calculations. 

Impact on Python Libraries 

Python libraries, while accessible and flexible, face specific challenges in mitigating rounding 
errors during high-precision computations[3]: 

Performance Overhead: Libraries like decimal and mpmath simulate arbitrary precision 
using software rather than hardware. This simulation involves multiple layers of abstraction, 
leading to substantial slowdowns, especially for computations requiring trillions of digits. For 
example: 

import mpmath 

mpmath.mp.dps = 1000  # Set precision to 1000 decimal places 

result = mpmath.mpf(1) / mpmath.mpf(7) 

Problem: While this approach achieves high precision, each operation carries an inherent 
performance cost, making Python less suitable for extremely large-scale computations. 

Limited Handling of Edge Cases: Even with advanced libraries, certain edge cases—such as 
calculations involving extremely large values or minuscule differences—introduce subtle 
rounding errors that are difficult to eliminate. These errors limit the reliability of Python for 
empirical verification of mathematical properties. 

 
 
 
 
 
 
 
Impact on C++ Libraries 

C++ libraries like GMP[4] and MPFR are known for their robustness in arbitrary precision 
arithmetic[6]. However, they too face notable challenges related to rounding errors: 

Dependency Chains: MPFR relies on GMP for its core arithmetic operations. If GMP 
introduces rounding errors in its calculations, these errors propagate through to MPFR-based 
computations. This dependency creates a cascading effect, amplifying inaccuracies in 
complex algorithms. 

Memory Constraints: High-precision computations often require the storage of large 
intermediate results. Insufficient memory can exacerbate rounding issues by forcing 
truncation or loss of precision. For instance: 

#include <gmpxx.h> 

mpf_class result(0, precision);  // Initialize GMP object with 
specified precision 

Problem: When memory is constrained, precision is sacrificed, directly impacting the 
accuracy of results in algorithms such as Chudnovsky. 

Conclusion on Rounding Errors 

The challenges posed by rounding errors[5] underscore the need for more robust approaches to 
arbitrary precision arithmetic. Modern hardware capabilities, including systems with high 
memory and processing power, present an opportunity to mitigate these issues. By developing 
libraries that: 

Minimize Rounding Errors: Implementing algorithms with enhanced error correction 
mechanisms to reduce cascading inaccuracies. 

Leverage Hardware Acceleration: Utilizing GPUs and multi-core CPUs to offset the 
performance overhead associated with software-based precision simulation. 

Optimize Memory Management: Ensuring efficient allocation and use of memory resources 
to handle large intermediate values without sacrificing precision. 

Addressing these challenges will significantly improve computational integrity and enable 
more reliable and scalable high-precision calculations across a range of disciplines. 

 
 
 
 
 
 
 
 
 
 
Call for Collaboration 

To address the myriad challenges associated with arbitrary precision computation, a 
collaborative and open approach is essential. Below is a detailed framework to tackle these 
challenges and foster advancements in computational tools: 

Open-Source Development 

The development of new Python libraries or the extension of existing ones, such as mpmath, 
represents a critical pathway forward. These efforts should prioritize the following: 

Unlimited Precision Support: Implement features that go beyond the current precision 
limitations, enabling the computation of trillions of digits without performance degradation. 

Hardware Acceleration: Leverage multi-threading, GPU processing, and other hardware-
based techniques to enhance performance and scalability. 

Community Feedback Integration: Design tools that actively incorporate feedback from 
users to ensure they meet the diverse needs of scientific and mathematical communities. 

By addressing these areas, new and improved Python libraries could become indispensable 
tools for both theoretical and applied research. 

C++ Optimization 

C++ remains a leading choice for high-performance computation due to its close-to-hardware 
capabilities. However, to overcome current limitations, the development of independent 
libraries must focus on: 

Bypassing GMP/MPFR Dependencies: Create standalone libraries that eliminate 
interdependencies, reducing memory management complexities and potential performance 
bottlenecks. 

Streamlined Memory Management: Implement advanced memory allocation strategies to 
manage large intermediate results efficiently. 

Full Hardware Utilization: Ensure libraries can harness the capabilities of modern high-
RAM systems, removing artificial constraints intended for legacy systems. 

By addressing these goals, C++ can remain competitive and continue to serve as a reliable 
foundation for precision-demanding computations. 

 
 
 
 
 
Community Involvement 

Collaboration is key to solving the challenges of arbitrary precision computation. Platforms 
like GitHub provide an ideal environment for fostering this collaboration. Key initiatives 
include: 

Sharing Optimized Scripts: Encourage the community to contribute well-documented and 
optimized scripts that demonstrate innovative solutions to common computational problems. 

Identifying and Addressing Bottlenecks: Collaborate to analyze and resolve the most 
pressing limitations in existing libraries and tools. 

Cross-Disciplinary Development: Develop libraries that cater to a range of scientific fields, 
from astrophysics to computational biology, ensuring versatility and broad applicability. 

Addressing the challenges of arbitrary precision computation requires a unified effort from 
the scientific and programming communities. By pooling expertise and resources, we can 
develop robust, scalable, and efficient tools that empower researchers across disciplines. 
These advancements will unlock new possibilities for discovery and innovation, ensuring that 
computational tools keep pace with the growing demands of modern science. 

Conclusion 

The challenges discussed in this paper are not merely technical limitations; they represent 
significant barriers to scientific progress. The shortcomings of current approaches to arbitrary 
precision computation, particularly in managing floating-point arithmetic rounding errors, 
inefficient library dependencies, and resource constraints, highlight the urgent need for 
innovative solutions. Modern hardware capabilities, such as abundant RAM and parallel 
processing, remain vastly underutilized, limiting the scalability and effectiveness of precision-
driven computations. 

Issues with Python Libraries 

Python, despite its popularity in scientific computation, demonstrates the difficulty of 
balancing accessibility with performance. Libraries like mpmath, decimal, and numpy offer 
extended precision but often do so at the cost of computational efficiency and scalability. 
These limitations force developers to rely on workarounds, such as embedding decimal 
within numpy, which create inefficiencies and hinder the libraries’ utility for large-scale 
projects. This duality between usability and performance underscores the need for libraries 
that prioritize both. 

Challenges in C++ Libraries 

C++ remains a powerful tool for high-performance computation, yet its prominent libraries, 
GMP and MPFR, introduce complexity through their interdependencies and memory 
management requirements. These limitations constrain the full exploitation of modern 
hardware and complicate the implementation of algorithms like Chudnovsky. A fresh 
approach to developing C++ libraries—one that emphasizes scalability, streamlined memory 
usage, and independence from rigid dependencies—is essential for progress. 

 
 
Opportunities for Advancement 

By addressing these issues, the scientific community stands to unlock significant 
advancements across multiple disciplines. Theoretical mathematics, astrophysics, and 
computational chemistry are just a few fields that rely on extreme precision and could benefit 
from modernized tools. Precision-driven computations, when adequately supported, can 
enable groundbreaking discoveries and innovations. 

A Call to Action 

To realize these opportunities, a collaborative effort is essential. Developers, researchers, and 
institutions must: 

- Contribute to open-source initiatives, such as the "Calculation of Number Pi" project, to 

share optimized algorithms and innovative solutions. 

- Advocate for the creation of libraries designed for today’s computational needs, leveraging 

modern hardware capabilities to their fullest. 

- Foster cross-disciplinary collaboration to ensure the resulting tools are versatile and address 

the diverse needs of the scientific community. 

Vision for the Future 

Modern computational science demands tools that can keep pace with its ambitions. By 
overcoming the limitations of current libraries and harnessing the potential of contemporary 
hardware, we can pave the way for a new era of precision-driven research. This paper serves 
as a call to action for the scientific community to come together, innovate, and build a 
foundation that empowers researchers to explore the furthest reaches of theoretical and 
applied sciences. 

Acknowledgments: I thank the open-source community for its efforts in advancing 
computational tools. This paper is a call to build on these foundations and push the boundaries 
of what is possible. 

 
 
 
 
 
 
 
 
 
 
References: 

1. A Detailed Proof of the Chudnovsky Formula with Means of Basic Complex Analysis: 
https://arxiv.org/abs/1809.00533 

2. Github repository: https://github.com/LinoCasu/CALCULATION_OF_NUMBER_PI 

3. Software Support for Arbitrary Precision Arithmetic in Programming Languages: 
https://www.ijcns.latticescipub.com/wp-content/uploads/papers/v3i2/A1425054124.pdf 

4. GMP Bignums vs. Python Bignums: Performance and Code Examples: 
https://jasonstitt.com/c-extension-n-choose-k 

5. Arbitrary-Precision Arithmetic (Wikipedia): https://en.wikipedia.org/wiki/Arbitrary-
precision_arithmetic 

6. Possibilities and Drawbacks Using Arbitrary Precision Numbers for Scientific Computing: 
https://publications.rwth-aachen.de/record/848030/files/848030.pdf 

View publication stats