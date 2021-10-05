# wenhua-college-email
文华学院(华中科技大学文华学院)电子信箱

---

### Pain Point
> **背景**：按照规定，edu.cn域名注册单位必须是我国依法设立的各级教育和科研单位。正是基于这一传统与管理要求，edu.cn域名被严格限定在国家相关部门批准设立的高校与科研院所范畴，网站是否采用edu.cn域名，已成为区分正规高校和冒牌、野鸡大学的重要标志。


当前文华学院使用的域名为`hustwenhua.net`,而使用文华学院主体注册的`whc.edu.cn`域名似乎并未按照规范使用。

| 域名 | 功能 |
|-------|:---------------------:|
|hustwenhua.net | 🎉文华学院主站 |
|whc.edu.cn | 😢文华云(三级域名下挂若干同集团其他学校项目) |

举一些例子：

- 英国高校一般都是「.ac.uk」域名
- 日本高校则一般都是「.ac.jp」域名
- 中国高校基本上都是「.edu.cn」域名

类似的，学生和教职工同样未能分配到`@whc.edu.cn`邮箱。这让相当一部分学生和教职工在各类场景受限：

- 期刊投递
- 海外院校申请
- 校园招聘网申
- JetBrains学生认证
- ...

### Possible Solution

- **PlanA**: 由学院官方层面推动`whc.edu.cn`替换原有域名并提供邮箱服务
- **PlanB**: 由计算机科学专业的同学或相关社团维护自治`@whc.ac.cn`邮箱

> `whc.ac.cn` 域名已为本repo预留

### How to do PlanB

> 该方案需要广泛的群众支持,以及可靠的域名邮箱服务.

贡献者Contributor贡献流程: 年级或班级负责人收集同学们的`学号,身份证后6位`信息,并串接盐`$SALT`进行`sha256`.提交到私密仓库Private-A.无论是仓库所有人/项目发起人/抑或是数据泄漏后得到该文件的黑客,均无法反推得到任何有效信息.

Github Action工作流程: 用户输入`学号,身份证后6位`,触发Action Workflow.对用户输入信息进行`sha256(input+$SALT)`匹配,Action Workflow使用Github Action Secrets内置密钥读取私密仓库Private-A内存放的加密数据.若匹配成功则触发后序步骤,通过HTTP接口激活该学号对应域名邮箱.

```
# How the data is collected by Contributor in Local
# 信息收集时刻，存于负责人本地的CSV表格
2020080855,190745
2020080856,056935
2020080857,572303
```

负责人得到维护者提供的盐`$SALT`用以`sha256`加密.
```
# How the data is encrypted by Contributor
# 负责人在本地对数据进行sha256+salt加密
sha256("2020080855,190745" + "SALT-#2f2fv234t34dcds$F#$@23242")
sha256("2020080856,056935" + "SALT-#2f2fv234t34dcds$F#$@23242")
sha256("2020080857,572303" + "SALT-#2f2fv234t34dcds$F#$@23242")
```

```
# How the data is pushed to Private-A repo by Contributor
# 负责人提交给项目组的内容为密文
69e3dfc89d320cab406ab4da1939643872e45bba36bd22be78214bc64fcbb8a7
a03c17e11eb75a578942ff69c840b552d14bd14bef7a96e74088419280cec534
0c8beae715850907dd7399af95482eb43151baa18f5ea9ed1a989fb589f07037
```

负责人删除本地原始信息.
