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
	
	begin																	-- This is not sequential code!!!
		-- sum of two product terms
		eq <= p0 or p1;			-- Output with result
		-- product terms
		p0 <= (not i0) and (not i1);	-- Condition 1
		p1 <= i0 and i1;		-- Or Condition 2
	end sop_arch;
 
![image](https://github.com/Ninja-Spotted/Portefolio/assets/105322822/52cedb30-cf90-42b5-ac8d-d0467b3d033f)

