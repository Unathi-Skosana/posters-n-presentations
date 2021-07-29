Hi My name is Unathi.

<br/>

I would like to talk a little bit about relative phase Toffoli gates, but before I can do that, I should attempt to give a bit of context and background.

<br/>

Perhaps, a basic definition we can start with is that of a computation, grotesquely simplified, is a mathematical abstraction which describes how a set of given input values can be composed with a given operation to give a set of output values. A computation is said to be classical when it is an abstraction of the physical evolution of a physical system whereby the evolution is governed by the "laws" of classical mechanics. And not strange enough, if this evolution is governed by the axioms of quantum mechanics, the computation is said be quantum.

<br/>

The simplest of such classical computational models is that of Boolean circuits, here the input/output values can take on only two possible values, which we might represent semantically as "0"/"off" & "1"/"on". Now Boolean circuits are a mathematical abstraction of digital logic circuits. In digital logic circuits, the two possible values are physically mapped to the HIGH/LOW voltage state of an electronic device called a transistor and operations, which are called logic gates in this language, are other electronic devices that can alter this HIGH/LOW voltage state in a controllable and deterministic manner, here the underlying physical phenomenon would be that of classical electromagnetism.

<br/>

Now that we've cleared away some of this terminology, we can get to kernel of the matter. In classical computation, the reversible Toffoli is a universal logic gate. It is reversible by the merit that the set of given input values under the operation of this logic gate can always be reconstructed from the set of output values; for those that are aware of Landauer's principle should appreciate why one would care whether such operations are reversible or not. It is universal by the merit that given any logic circuit that performs some Boolean operation, it is possible to convert it to another logic circuit, that is equivalent in operation, and only made up of Toffoli gates.

<br/>

I give a schematic diagram of the doubly-controlled Toffoli gate and its truth table in Figure. 1, which describes the operation of the Toffoli gate. If we take a close look at the table, we see that the doubly-controlled Toffoli flips the third input value, if the first two input values are in the "1" state, otherwise it leaves the input values unchanged and this is the very reason why it is called a doubly-controlled Toffoli, that is the two input values control what happens to the third input value.

<br/>

Now the classical Toffoli gate, can be realized as a quantum logic gate, due to it being reversible, in the jargon of quantum mechanics, such a reversible operation is said to be a unitary operation. As a quantum logic gate, though not universal on its own for quantum computation, it plays a quite pivotal role in the realization of Boolean arithmetic across quantum logical registers and ensures that quantum computation actually subsumes classical computation, if this wasn't the case, quantum computers would probably be superfluous.

<br/>

What I show in equation 1, is a convenient notation that conveys the same information already contained in Figure 1, it describes the action of a doubly-controlled Toffoli gate, which we denote by CCX given a set of input values $a,b,c$

<br/>

Notwithstanding their apparent importance, quantum Toffoli gates are far from simple to realize on physical quantum hardware and for this reason they are not natively supported but rather the physical quantum hardware implements a universal gate set made up of a few single qubit gates (X, RZ, S) and a single two-qubit entangling gate (CX, CZ and so on) and then a Toffoli gate decomposes in terms of this universal gate set. For instance, there's a standard result that says that you cannot implement $n$-controlled Toffoli gate with less than $2n$ two-qubit gates, thus a doubly controlled Toffoli gate decomposes into six CX and seven $T/T^{\dagger}$ gates.

<br/>

However, this way of doing things comes with its own perils. Due to the considerable effects of noise n' decoherence on current quantum hardware, which place an upper limit on the number of gates, particularly two-qubit entangling gates, that can be in a quantum circuit, so that its actual operation fairly approximates its ideal operation and is distinguishable from random noise.

<br/>

For this reason, this makes the study of Toffoli gates and their decompositions in terms of universal gate sets, a subject of interest for near-time practical quantum computing, and the main conception of this study is in the same spirit.

<br/>

We particularly looked at the use of relative phase Toffoli gates, which are variants of Toffoli gates whose operation is equivalent to that of a Toffoli gate modulo an undesirable relative phase shift. What is peculiar to these gates is that they're smaller in circuit size, for instance the Margolus gate decomposes into $3$ CX gates and $12$ single qubit gates, and it has been shown that this decomposition is optimal.

<br/>

Due to the undesirable relative phase shift of such a gate, it was held that they would be of very little utility beyond the commonly conceived scenarios, for instance it was held that these gates would only be of use if for some specific reason relative phase shifts didn't matter or the gates were being applied last, but since then they have been used extensively to improve decompositions of certain multiply-controlled Toffoli configurations while preserving their functional correctness.

<br/>

Next to demonstrate what one can do with such a gate, we consider a small pedagogical example that compares and assess the performance of the Margolus gate and a doubly-controlled Toffoli gate on IBM's superconducting quantum processor, ibmq_casablanca.

<br/>

We specifically choose an example state which we prepare with both a Toffoli and Margolus gate, in such a way that we generate an output state that is ideally entangled. Via quantum state tomography, it is possible to recover an approximation of this state that is actually prepared on the processor and compare it to the ideal state that would've been prepared if the operation of the processor was ideal.

<br/>

What you see on Figure 2. are these reconstructed states, (a) and (b) are real and imaginary parts of the actual state when it is prepared with a Toffoli gate and similarly (c) and (d) when it is prepared with a Margolus gate.

<br/>

A more quantitative comparison between the two is that of state fidelity; which for many purposes can be thought of as quantifying closeness/distance between two quantum states, notwithstanding that it isn't true distance metric.

<br/>

For the two states in Figure 2. we measured, within 95% confidence intervals to be the numbers I show there. We observe is that the Margolus gate, prepares a state that is closer to the ideal state of Equation. 4 better than the full Toffoli gate.

<br/>

It is possible, although much harder (computation-wise), to asses the performance of a quantum gate in a much thorough way, via quantum process tomography. The aim of quantum process tomography, is not very different from that of quantum state tomography, here we seek to estimate a quantum channel that describes the actual operation of a quantum circuit on a particular quantum processor.

<br/>

What we can reconstruct from quantum process tomography, is the chi-matrix representation of a quantum channel, which is a matrix such that the quantum channel evolves a given quantum state rho as shown in Equation. 6.

<br/>

Having gotten this, we can measure a quantity called the average gate fidelity shown in Equation. 5, which measures how close/how well this reconstructed quantum channel approximates the ideal operation of the quantum channel. We show the measured average gate fidelities within 95% confidence intervals for the respective circuits. Again we see that the circuit which prepares the state in Equation. 4 with a Margolus gate is better reconstructed than the one which prepares it with a full Toffoli gate.

<br/>

Having learned all these things about relative Toffoli gates, we undertook a case study of Shor's quantum factoring algorithm in which Toffoli gates heavily feature. I will attempt to summarize the important bits of Shor's algorithm for prime factorization. The essence of Shor's quantum algorithm is that it reduces the problem of finding the prime factors of a composite integer to that of finding an integer $r$ called the order, which can then be used to factor a composite integer into its prime constituents.

<br/>

In Figure 4, I show a schematic of the order-finding routine in Shor's algorithm for $n$ qubits. The number of qubits in the control register, which is at the top, determines the bit accuracy of the extracted order, and the work register, at the bottom, encodes the composite integer $N$ that is to be factored. At the beginning both registers are initialized appropriately, then controlled modular exponentiation operation is performed and lastly the inverse quantum Fourier transform is applied to the control register and computational basis measurement is performed.

<br/>

The reason why Shor's algorithm for prime factorization has captivated the minds of computer scientists and physicists alike, is that theoretically it performs exponentially better than the best known classical algorithm for prime factorization in terms of algorithm time complexity! This might not sound all that interesting, until you consider the fact that the rationale behind the RSA public-key encryption system as used on the Internet today, is that the problem of prime factorization is a difficult one; well Shor's algorithm seems to suggest otherwise, at least theoretically.

<br/>

In practice, Shor's algorithm is still quite far off from posing any real threat to the RSA encryption system, as alluded to already is that the effects of noise on current quantum hardware severely limit the size of quantum circuits that can be executed reliably. What researchers of such things today, are interested in, are approaches to designing new or existing quantum algorithms in a manner that is aware of the limitations of current hardware and attempts to mitigate these limitations in some way or another. As the last bit of this poster, I will present three, including our own, of such recent developments in the case of Shor's algorithm.

<br/>

In 2012, and 2019, the integer $N=21$ was factored into prime constituents (which are $3$ and $7$ in case anyone is wondering), setting the record for the largest integer factored with Shor's algorithm on quantum hardware. Both schemes perform the algorithm in a way that's peculiar to them, for the first scheme of Martin-Lopez performs the algorithm iteratively, what this means that the control register can be reduced to be the size of one qubit; via real-time conditionals and feed forward operations this qubit is recycled and reused on each iteration, the bit-accuracy of the extracted order is determined by the number of such iterations. Furthermore, the work register of this scheme uses a single qutrit rather than five qubits, making the system a hybrid qubit-qutrit system. This is way of doing things is advantageous due to great reduction in the number of qubits used, which are hard to come by and number of gates.

<br/>

Secondly, this scheme in its decomposition of the modular exponentiation operation, uses full Toffoli gates, which as we've seen are quite expensive operations even for a qubit-qutrit system. Now an interesting point to us, and probably a consequence of the previous point, is that full factoring was not achieved. The scheme falls one iteration short of fully factorizing $N=21$ via continued fractions. 

<br/>

The second scheme of Amico takes an pseudo-iterative approach, I say, pseudo, because each iteration is not done with real-time conditionals and feed-forward operations but rather via splitting each iteration as a separate circuit and thus manually reseting the entire computation each time. This scheme however, also uses effectively via this pseudo-iterative method a single qubit in the control register and five qubits in the work register, and also uses full Toffoli gates in its decomposition of the modular exponentiation operation. Finally, what is peculiar to this scheme is that the order is not extracted via continued fractions, but rather inferred via a statistical test.

<br/>

Our scheme, which is different to both in operation, is not iterative and uses three qubits in the control register. Inspired by the first scheme, we compensate for this gain in number of qubits in the control register, by mapping the qutrit system of the first scheme onto a two-qubit system, which means our work register uses only two qubits instead of five.

<br/>

At first sight, it would seem that taking a non-iterative approach would hinder the successful execution of the algorithm. However, we were able to decompose the modular exponentiation operation in terms of relative phase Toffolis while preserving its functional correctness, which led to a great reduction in the number of gates in our circuit, by a factor of half for two-qubit gates. This reduction allowed us to fully factorize $N=21$ via continued fractions, without the need for any statistical tests, and additionally we were able to verify entanglement across the two registers in the circuits, which is deemed to be a requisite for the successful operation of the algorithm.

<br/>


In summary, through the use of relative phase Toffoli gates, we were able to go beyond the demonstration of Martin-Lopez in fully factoring $N=21$. We implemented the algorithm on IBM quantum processors using only five qubits, successfully verifying the presence of entanglement between the control and work register qubits, which is a necessary condition for the algorithm's speedup in general. The techniques we employ may be useful in carrying out Shor's algorithm for larger integers, or other algorithms in systems with a limited number of noisy qubits.

<br/>

Thank you for listening.
