# L / R / M

L/R/M là thứ tự box in-scope theo XML của từng frame.

## adasind_060000.jpg
- L3+R10+M5: LRM (mid)
- L4+R6+M8: LRM (mid)
- L8+R4: LR_noM (edge)
- L5+R2: LR_noM (mid)
- L7+R3: LR_noM (center)
- L9+R8: LR_noM (center)
- L6+R1: LR_noM (center)
- L2+R7+M6: LRM (center)
- L1+R5+M4: LRM (mid)
- R9: R_only (center)
- M2: M_only (mid)
- M3: M_only (mid)
- M7: M_only (mid)
- M9: M_only (center)
- M10: M_only (center)
- M11: M_only (center)
- M12: M_only (center)
## adasind_086220.jpg
- L6+R1: LR_noM (mid)
- L4+R5: LR_noM (mid)
- L2+R2+M1: LRM (center)
- L1+R3+M4: LRM (center)
- L3: L_only (center)
- L5: L_only (mid)
- R4: R_only (center)
- M2: M_only (center)
- M3: M_only (center)
- M5: M_only (mid)
- M6: M_only (mid)
- M7: M_only (mid)
- M8: M_only (center)
## adasind_102750.jpg
- L5+R3: LR_noM (mid)
- L2+R1+M1: LRM (mid)
- L4+R4: LR_noM (edge)
- L1: L_only (mid)
- L3: L_only (edge)
- L6: L_only (center)
- R2+M2: RM_noL (edge)
- R5+M8: RM_noL (center)
- M3: M_only (mid)
- M4: M_only (mid)
- M5: M_only (mid)
- M6: M_only (center)
- M7: M_only (mid)

## Zone × cell
| zone | LRM | LR_noM | LM_noR | L_only | RM_noL | R_only | M_only |
|---|---|---|---|---|---|---|---|
| center | 3 | 3 | 0 | 2 | 1 | 2 | 8 |
| mid | 4 | 4 | 0 | 2 | 0 | 0 | 10 |
| edge | 0 | 2 | 0 | 1 | 1 | 0 | 0 |
