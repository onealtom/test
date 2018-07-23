## 第一题 ##
有一个API头文件中定义了一个结构体数据，在某次更新后头文件发生了变化，下面是这个头文件补丁的差异文件（减号是删除的行，加号是添加的行）：
```c
typedef struct skb_frag_struct skb_frag_t;
  
struct skb_frag_struct {
 -	struct page *page;
 +	struct {
 +		struct page *p;
 +	} page;

	__u32 page_offset;
	__u32 size;

};

```
由于头文件的数据定义发生了变化，所以调用API的程序也需要修改，下面是更新之前的调用程序：
```c
static inline struct page *skb_frag_page(const skb_frskb_frag_tag_t *frag)
{
    return frag->page;
}

static inline void __skb_frag_set_page(skb_frag_t *frag, struct page *page)
{
    frag->page = page;
}
```
应该如何修改？
```c
static inline struct page *skb_frag_page(const skb_frskb_frag_tag_t *frag)
{
                              /*填入你的答案*/
}
static inline void __skb_frag_set_page(skb_frag_t *frag, struct page *page)
{
                              /*填入你的答案*/
}
```

## 第二题 ##
下面是一个电路示意图，
```
 MEM Ctrl                  NOR Flash
+-------+                 +--------+
|       |                 |        |
|  DAT0 <-----------------> DAT0   |
|  DAT1 <-----------------> DAT1   |
|  DAT7 <-----------------> DAT2   |
|  DAT2 <-----------------> DAT3   |
|  DAT4 <-----------------> DAT4   |
|  DAT5 <-----------------> DAT5   |
|  DAT6 <-----------------> DAT6   |
|  DAT3 <-----------------> DAT7   |
|  DAT16<-----------------> DAT8   |
|  ...  |     +---+       | ...    |
|   A19 +-----|NOT|o------> #CS    |
|       |     +---+       |        |
+-------+                 +--------+
```

- [x] 判断下面的描述是否正确，对的在前面的框中打钩，错的打叉：
- [ ] 不应该用内存控制器连Flash
- [ ] DAT7<->DAT2连错
- [ ] DAT2<->DAT3连错
- [ ] DAT3<->DAT7连错
- [ ] DAT16<->DAT8连错
- [ ] A19地址线不能连CS
- [ ] 地址线连CS不应该加非门
- [ ] 其他错误：


## 第三题 ##
烧一根不均匀的绳子，从头烧到尾是要1个小时。现在有若干条材质相同的绳子问如何用烧绳的方法来计时一个小时15分钟。

## 第四题 ##

C语言写一个Hello Wrold程序，然后用arm-linux-gnueabihf-gcc交叉编译，指定使用linaro gcc 4.7版本。

## 第五题 ##

按http://ishare.iask.sina.com.cn/f/14523642.html 将文档中web服务器在PC上编译配置搭建好。

## 第六题 （现场实验题）##

这里有一个驱动源码

https://github.com/analogdevicesinc/no-OS.git
现需要将no-OS/ad9361/sw/main.c 中的main()函数改名位ad936x_init()函数，并移植到一个STM32环境中编译，再调用API函数，获取当前本振Local Oscillator频率。
提示信息：
1. 建议使用keil
2. 底层spi port函数可以留空
3. API函数在ad9361_api.h中
4. STM32型号任意，主要考查过程
