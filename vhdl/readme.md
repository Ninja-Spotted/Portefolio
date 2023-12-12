---
title: "VHDL"
permalink: "/VHDL"
has_children: true
layout: default
---

## Quick VHDL reference manual I put together for personal use. 

VHDL is a general and flexible language for describing and modeling a digital system.

IEEE Standard Multivalue Logic System for VHDL Model Interoperability
• IEEE Std 1164-1993

### VHDL design descriptions

VHDL design description = ENTITY declaration + ARCHITECTURE body

- Entity --> design **I/O**
- Architecture --> Content or functionality of entity
  - Structural --> Set of interconnected components
  - Functional or Dataflow --> Flow of data expressed using concurrent signal assignment statements
  - Behavioral --> Set of statements that are executed **sequentially** in the specified order

 Every architecture need an entity so it is usual to refer them as an ENTITY/ARCHITECTURE PAIR.

### One Bit Comparator

 ![image](https://github.com/Ninja-Spotted/Portefolio/assets/105322822/7fe8d577-14af-4efd-98d0-7a8b498cb999)

Can be described as a sum of products: eq = /i0 . /i1 + i0 . i1

#### Gate-level Description (Functional or Dataflow):

	library ieee;
	use ieee. std_logic_1164. all ;		-- VHDL Standard


	entity eq1 is				-- I/O of the comparator
		port (
			i0, i1: in std_logic;	-- 2 Inputs
			eq: out std_logic	-- 1 Output
		) ;
	end eq1;

	architecture sop_arch of eq1 is		-- Association ENTITY/ARCHITECTURE
		signal p0, p1: std_logic;	-- Definition of internal signals ("variables")
	
	begin					-- This is not sequential code!!!
		-- sum of two product terms
		eq <= p0 or p1;			-- Output with result
		-- product terms
		p0 <= (not i0) and (not i1);	-- Condition 1
		p1 <= i0 and i1;		-- Or Condition 2
	end sop_arch;
 
![image](https://github.com/Ninja-Spotted/Portefolio/assets/105322822/52cedb30-cf90-42b5-ac8d-d0467b3d033f)

#### Entity declaration

- IN --> Signal/data goes into the entity only
- OUT --> signal/data goes out of the entity only (and is not used internally)
- INOUT --> signal/data is bi-directional (goes into and out of the entity)
- BUFFER --> signal/data that goes out of the entity and is also fed-back internally

#### Data Types
- IEEE.STD_LOGIC_1164.ALL
  - STD_LOGIC, STD_LOGIC_VECTOR, STD_ULOGIC, and STD_ULOGIC_VECTOR
- IEEE.NUMERIC_STD.ALL
  - SIGNED, UNSIGNED, INTEGER, plus several data conversion functions

### 2-bit Comparator

Using the same structure as before:

	library ieee;
	use ieee. std_logic_1164. all ;
 
	entity eq2 is
		port (
			a, b: in std_logic_vector(1 downto 0);
			aeqb: out std_logic
		) ;
	end eq2;
 
	architecture sop_arch of eq2 is
		signal p0, p1, p2, p3: std_logic;
 
	begin
		aeqb <= p0 or p1 or p2 or p3; -- sum of four product terms
		-- product terms
		p0 <= ((not a(1)) and (not b(1))) and ((not a(0)) and (not b(0)));
		p1 <= ((not a(1)) and (not b(1))) and (a(0) and b(0));
		p2 <= (a(1) and b(1)) and ((not a(0)) and (not b(0)));
		p3 <= (a(1) and b(1)) and (a(0) and b(0));
	end sop_arch;

#### Instantiation

![image](https://github.com/Ninja-Spotted/Portefolio/assets/105322822/6873aee8-53a5-4eb6-94d5-1c47544f67f2)

Enables to build large systems from simpler or predesigned components --> structural description

	architecture struc_arch of eq2 is				-- Association ENTITY/ARCHITECTURE
		signal e0, e1: std_logic;				-- Definition of internal signals ("variables")
	
	begin
		-- instantiate two 1-bit comparators
		eq_bit0_unit: entity work.eq1 (sop_arch)		-- Define the structure used in instantiation (1-bit comparator building block)
			port map (i0 => a(0), i1 => b(0), eq => e0);	-- inside-block => outside-block (bit 0)
		eq_bitl_unit: entity work.eq1 (sop_arch)
			port map (i0 => a(1), i1 => b(1), eq => e1);	-- inside-block => outside-block (bit 1)
		-- a and b are equal if individual bits are equal
		aeqb <= e0 and e1;
	end struc_arch;
