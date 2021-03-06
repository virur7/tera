# C++ SDK接口重构

# 目标

  * 提升接口可读性，降低找接口时间
  * 精简接口，提升注释
  * 降低用户误用接口的概率
  * 内部与接口代码分离
  * 保证与旧代码的兼容
 
# 原SDK

  * 截至0.5版本
  * 所有接口全部在一个头文件（tera.h）里
   * 代码过长，很难找到相要的接口
   * 不同类的使用频度不同，放在一起会让更重要的类被淹没（比如Client/Table等）
   * 代码层次感弱一点，文件名也是代码的重要一部分
   
# 新SDK结构

  * 最外层增加一个include目录，表示对外接口
   * tera.h移至此目录
   * tera_easy.h/tera_ha.h等移至此目录
   * 编译时，生效至build目录
  * tera.h
   * 拆分成若干文件，按对象、功能划分文件
   * tera.h自身变成一个入口，使用时依然只需要include一个文件
  * 每个类内部（Table/Client/RowMutation等）
   * 按接口使用频率重新排序
   * 接口分类
    * 默认为已发布接口
    * DEVELOPING 开发中接口，鼓励完善    
    * EXPERIMENTAL 正在测试中，鼓励试用
    * DEPRECATED 未实现或不建议用户使用，保证兼容性
  * 重写接口注释
