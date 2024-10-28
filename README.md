## Build Setup

### install dependencies

```
npm install
```

### serve with hot reload at localhost:8080

```
npm run dev
```
Đang dùng fake data nên display rất là ngu 
``` 
VideoDisplay 

const videoContext = require.context('@/assets/videos', false, /\.(mp4|webm|ogg)$/); để lấy video trực tiếp từ assets để display trên web

```

```
Dashboard aka Home

data hiện tại đang load qua "/public/data.json" vì đang ko dùng database. Fetch xong load vào 3 cái process (đang dùng tên template lười sửa) 

activityChart là error tổng số error mỗi ngày, filter fake thôi chưa hoạt động đâu

processUsersChart là error trong ngày hôm đấy xem, hơi trùng với chart đầu, ko hiện j vì fake data mới chỉ đến 27/10/2024

PreferencesChart là percentage total error, đang chưa hoạt động theo dự kiến tí ehe 