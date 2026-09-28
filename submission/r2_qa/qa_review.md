# QA review · B4-dense

Mã khóa: AEBB-D053

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_258420.jpg | L1 | R04 | Box bao trọn một xe ba bánh (auto-rickshaw, thân vàng/đen, kính chắn gió hẹp) đang gán class `Car`; theo R04 xe ba bánh chở người/hàng phải là `ThreeWheeler`. |
| adasind_258420.jpg | L2 | R04 | Box bao xe ba bánh (auto-rickshaw mui hồng/vàng, đậu bên phải) đang gán class `Car`; theo R04 nên là `ThreeWheeler`. |
| adasind_258420.jpg | L7 | R04 | Box ở rìa trái ảnh bao một xe dáng ba bánh (thân tối màu, khoang chở phía sau) đang gán class `Car`; theo R04 nên là `ThreeWheeler`, cần zoom kỹ thêm để chắc chắn vì bị cắt một phần ngoài khung. |
| adasind_270517.jpg | L2 | R04 | Box bao xe ba bánh (tuk-tuk thân tối, khoang lái hẹp, đuôi vuông) đang gán class `Car`; theo R04 nên là `ThreeWheeler`. |
| adasind_270517.jpg | L8 | R04 | Box lớn bao xe ba bánh mui vàng đang dừng bên đường, đang gán class `Car`; theo R04 nên là `ThreeWheeler`. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
