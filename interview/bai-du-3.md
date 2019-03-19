# 百度3

### 编程题

1. NMS

{% hint style="danger" %}
NMS都不会,做什么detection.

> [From知乎](https://www.zhihu.com/question/286925266/answer/491117602)

望共勉
{% endhint %}

非极大值抑制\(Non-Maximum Suppression, NMS\)，顾名思义就是抑制那些不是极大值的元素，可以理解为局部最大值搜索。对于目标检测来说，非极大值抑制的含义就是对于**重叠度**较高的一部分同类候选框来说，去掉那些**置信度**较低的框，只保留置信度最大的那一个进行后面的流程，这里的重叠度高低与否是通过 NMS **阈值**来判断的。



```cpp
#include <iostream>
#include <vector>
#include <algorithm>

struct Bbox {
    int x1;
    int y1;
    int x2;
    int y2;
    float score;
    Bbox(int x1_, int y1_, int x2_, int y2_, float s):
	x1(x1_), y1(y1_), x2(x2_), y2(y2_), score(s) {};
};

float iou(Bbox box1, Bbox box2) {
    float area1 = (box1.x2 - box1.x1 + 1) * (box1.y2 - box1.y1 + 1);
    float area2 = (box2.x2 - box2.x1 + 1) * (box2.y2 - box2.y1 + 1);

    int x11 = std::max(box1.x1, box2.x1);
    int y11 = std::max(box1.y1, box2.y1);
    int x22 = std::min(box1.x2, box2.x2);
    int y22 = std::min(box1.y2, box2.y2);
    float intersection = (x22 - x11 + 1) * (y22 - y11 + 1);

    return intersection / (area1 + area2 - intersection);
}

std::vector<Bbox> nms(std::vector<Bbox> &vecBbox, float threshold) {
    auto cmpScore = [](Bbox box1, Bbox box2) {
	return box1.score < box2.score; // 升序排列, 令score最大的box在vector末端
    };
    std::sort(vecBbox.begin(), vecBbox.end(), cmpScore);

    std::vector<Bbox> pickedBbox;
    while (vecBbox.size() > 0) {
        pickedBbox.emplace_back(vecBbox.back());
        vecBbox.pop_back();
        for (size_t i = 0; i < vecBbox.size(); i++) {
            if (iou(pickedBbox.back(), vecBbox[i]) >= threshold) {
                vecBbox.erase(vecBbox.begin() + i);
            }
        }
    }
    return pickedBbox;
}

int main() {
    std::vector<Bbox> vecBbox;
    vecBbox.emplace_back(Bbox(187, 82, 337, 317, 0.9));
    vecBbox.emplace_back(Bbox(150, 67, 305, 282, 0.75));
    vecBbox.emplace_back(Bbox(246, 121, 368, 304, 0.8));

    auto pickedBbox = nms(vecBbox, 0.5);

    for (auto box : pickedBbox) {
	std::cout << box.x1 << ", " <<
		box.y1 << ", " <<
		box.x2 << ", " <<
		box.y2 << ", " <<
		box.score << std::endl;
    }
    return 0;
}
```

> Refer to :[从零开始的BLOG](https://hellozhaozheng.github.io/z_post/%E8%AE%A1%E7%AE%97%E6%9C%BA%E8%A7%86%E8%A7%89-NMS-Implementation/)

