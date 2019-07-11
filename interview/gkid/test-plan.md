

# GKid App Test Plan

## Tests includes

UI Test - 验证功能正确性

* Appium + Maven + Selenium + ...

Interface Test - 验证接口

* http api
* 正确性，安全性，稳定性（异常值）
* 数据传入，数据返回
* 自动化持续集成
* 基本功能，边界值，性能
* 结果展示，定位问题，代码覆盖率
* 业务功能，业务规则，参数验证，接口异常，性能，安全

* app.gkid.com

Performance Test

...

## Interface Test

### app 打开

* get /api/gkids/version/feature?version=1.4.4&gkidno=10869684

```json
{ 
  ...
  need_to_upgrade=False
  ...
}
```

* get /api/gkids/course_list

```json
{
  available_course: [] // 体验课，系统课
  package: [] // 启蒙，进阶...
  plans: [] // 月课，体验课
}
```

* get /api/gkids/client_log_presign
* get /api/gkids/device
* get /api/ext/client_log

### 体验课

* POST api/gkids/smart_trail_course_list_v2

```json
{
  front_page
  menu_page
}
```

* POST api/gkids/event_track 

用户行为

### 系统课

* POST /api/gkids/smart_course_list_all_v2

### 购买课程

* GET /api/gkids/user/address
* GET /aip/gdkis/class_availability?level=1&duration=4&course_type=reading

```json
{
  avail_num=62
  class_info
  total_allowed=150
  total_current=88
}
```

* GET /api/gkids/user/…../course_coupons?duration=4

```json
{
  amount=20000
  ...
}
```

## 绘本

* GET /api/gkids/class/picture_books?tab=0...

```json
{
  picture_books:[
    cover_url=
    id=
    rate=
  ]
  read_count=0
  total=0
}
```

* POST /api/gkids/ai/upload/ai_event

### tab1

GET /api/gkids/class/picture_books?tab=1

### 打开绘本

* /api/gkids/class/picurebook/….

```json
{
  audio_url
  cover_url
  pages:[
    audio_url
    image_url
    text
  ]
...
}
```

## 用户模块

* GET /api/gkids/user/ongoing_course
* GET /api/gkids/user/purchased
* GET /api/gkids/user/
* GETGET /api/gkids/user/…/coupons