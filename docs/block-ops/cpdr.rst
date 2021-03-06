CPDR
--------

**CPDR**
	Compare and Decrement with Repeat

**Description**
	| Performs ``cpd`` until either ``A`` = ``(HL)`` or ``BC`` = 0.

		.. code-block:: asm

			cp a,(hl)
			dec hl
			dec bc
			jr nz,-7
			ret po
			jr -10

**Uses**
	- Finding a certain letter in a string (or other similar tasks)

**Results**
	================    ==========================================  ========================================
	Register/Flag       16-bit (non-ADL)                            24-bit (ADL)
	================    ==========================================  ========================================
	``S`` flag          Set if result is negative; else reset
	----------------    ------------------------------------------------------------------------------------
	``Z`` flag          Set if ``A`` = ``(HL)``; else reset
	----------------    ------------------------------------------------------------------------------------
	``H`` flag          Set if borrow from bit 4; else reset
	----------------    ------------------------------------------------------------------------------------
	``P/V`` flag        Set if ``BC`` ≠ 0 after the operation; else reset
	----------------    ------------------------------------------------------------------------------------
	``N`` flag          Set
	----------------    ------------------------------------------------------------------------------------
	``C`` flag          Not affected
	================    ====================================================================================

**Allowed Instructions**
	================  ================  ===========================================================================================================================================  ==============================  ==============================
	Instruction       Opcode            CC (ADL/non-ADL)                                                                                                                             CC (.S)                         CC (.L)
	================  ================  ===========================================================================================================================================  ==============================  ==============================
	cpir              $ED, $B1          ``2F + (Iterations)*(1R + 2) - 1`` where ``Iterations`` is the number of iterations of ``cpd`` before either ``A`` = ``(HL)`` or ``BC`` = 0  3F + (Iterations)*(1R + 2) - 1  3F + (Iterations)*(1R + 2) - 1
	================  ================  ===========================================================================================================================================  ==============================  ==============================

**Notes**
	- Interrupts can be triggered while this instruction is in progress (unless they are disabled using ``DI``, of course).

**See Also**
	`CP </en/latest/docs/arithmetic/cp.html>`_, `CPD <cpd.html>`_, `CPI <cpi.html>`_, `CPIR <cpir.html>`_, `LDDR <lddr.html>`_
