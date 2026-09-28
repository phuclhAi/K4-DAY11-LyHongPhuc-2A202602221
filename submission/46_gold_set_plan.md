# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Người đi bộ/xe máy cắt ngang giao lộ, ngược sáng lúc bình minh/hoàng hôn | Contrast thấp + chuyển động ngang tốc độ cao dễ miss hoặc trễ box | Vòng kính, tiêu cự và mốc lens_border của camera front tại thời điểm chụp | Ít nhất 2 người soát độc lập bằng luật, đối chiếu ảnh gốc trước khi gán gold |
| rear | Vật thấp/trẻ em sát cản sau khi lùi, khuất bởi cấu trúc xe (móc kéo, cản) | Vùng gần đáy khung dễ bị ego_body che một phần, kích thước box nhỏ dưới ngưỡng H=40px | Calibration khoảng cách gần (near-field) và ranh giới ego_body đã vẽ | Soát tay kèm zoom vào vùng gần đáy khung, so với ảnh gốc độ phân giải đầy đủ |
| left | Xe máy/xe đạp áp sát điểm mù khi chuyển làn, chồng lấn với seam front-left | Vật ở rìa vòng kính (zone edge) méo mạnh, dễ nhầm class hoặc box lệch | Calibration seam left↔front, left↔rear và mốc thời gian đồng bộ giữa hai camera | Review riêng theo từng camera trước, chỉ ghép seam khi có timestamp + policy xác nhận |
| right | Người đi bộ/xe đạp sát vỉa hè tại điểm đón-trả khách, chồng seam right-rear | Mật độ vật thể cao cục bộ (dense), dễ trùng lặp hoặc bỏ sót khi vật chồng nhau | Calibration seam right↔rear và vùng ignore_region riêng của camera right | Đối chiếu tối thiểu 2 lượt soát độc lập cộng kiểm tra logic seam trước khi chốt gold |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): refresh khi thay đổi phần cứng/góc lắp camera (calibration đổi), khi rules v1.0.0 được vá (guideline patch), hoặc khi phát hiện tỷ lệ lỗi hệ thống (systematic error) vượt ngưỡng chấp nhận ở một zone/camera cụ thể trong quá trình rework.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: một vật xuất hiện ở rìa camera front và rìa camera left cùng lúc (ví dụ người đi bộ băng qua góc xe) — chỉ ghép thành một track/ID khi có timestamp đồng bộ giữa hai camera, calibration cho biết vùng chồng hình học thực tế, và ảnh chụp cho thấy cùng một vật chứ không phải hai vật giống nhau; nếu thiếu một trong ba, giữ hai box riêng và escalate.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera: dữ liệu thực hành hiện chỉ có ảnh của **một** camera fisheye (ADASIND); agreement cao trên camera này không nói lên gì về độ méo, góc lắp, hay điều kiện ánh sáng khác nhau của front/rear/left/right thật, và không kiểm chứng được logic ghép seam giữa các camera — cần dữ liệu thật của cả bốn camera mới xác nhận được.
