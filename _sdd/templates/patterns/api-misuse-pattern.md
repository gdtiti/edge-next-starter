# API误用调试模式

## 🎯 适用场景
第三方库API使用错误，包括：
- API返回undefined或意外值
- 类型错误或运行时异常
- 功能行为不符合预期
- 文档与实际行为不一致

## 🔍 问题识别清单
- [ ] API调用返回undefined或null
- [ ] TypeScript类型错误
- [ ] 运行时异常或错误
- [ ] 功能结果不符合预期
- [ ] 性能问题或超时

## 🧠 根因分析（5 Whys模板）

### 第一轮：现象分析
1. **为什么API返回错误？** → 字段名不正确或API使用方式错误
2. **为什么字段名不正确？** → 文档过时、理解错误或版本不匹配
3. **为什么没有发现错误？** → 缺少类型检查或测试覆盖不足
4. **为什么缺少类型检查？** → 依赖库类型定义不完整或配置不当
5. **为什么没有验证？** → 开发流程缺少验证步骤或质量门禁

### 第二轮：深度分析
1. **为什么选择这个API？** → 技术选型不当或调研不充分
2. **为什么调研不充分？** → 时间压力或经验不足
3. **为什么没有备用方案？** → 过度依赖单一解决方案
4. **为什么没有错误处理？** → 开发习惯或团队规范缺失
5. **为什么没有及时发现？** → 测试策略不完善

## 🛠️ 解决方案设计

### 方案A：修复API使用（推荐）
**优点**：
- 保持现有架构
- 学习成本最低
- 影响范围最小

**实施步骤**：
1. 深入研究API文档和源码
2. 修正字段名或调用方式
3. 添加TypeScript类型定义
4. 实现错误处理和降级方案
5. 编写单元测试验证

**风险评估**：
- 低风险：主要是代码修正
- 中等工作量：需要详细测试

### 方案B：替换API或库
**优点**：
- 可能获得更好的功能
- 避免类似问题

**缺点**：
- 高迁移成本
- 引入新的不确定性
- 学习成本高

**适用场景**：
- 当前API确实无法满足需求
- 有更好的替代方案
- 时间和资源充足

### 方案C：封装适配层
**优点**：
- 隔离第三方依赖
- 便于未来替换
- 可以添加额外功能

**缺点**：
- 增加复杂度
- 性能开销
- 维护成本

## 📋 验证检查清单

### 功能验证
- [ ] API调用返回正确结果
- [ ] 所有边界情况处理正确
- [ ] 错误情况有合适的降级方案
- [ ] 性能满足要求

### 类型安全验证
- [ ] TypeScript编译无错误
- [ ] 所有API返回值有类型定义
- [ ] 空值处理完整
- [ ] 严格模式检查通过

### 测试验证
- [ ] 单元测试覆盖主要场景
- [ ] 集成测试验证完整流程
- [ ] 错误场景测试覆盖
- [ ] 性能测试通过

## 🛡️ 预防措施

### 开发流程
1. **API调研阶段**
   - [ ] 阅读官方文档和示例
   - [ ] 检查社区评价和使用情况
   - [ ] 验证版本兼容性
   - [ ] 创建概念验证（POC）

2. **集成阶段**
   - [ ] 添加TypeScript类型定义
   - [ ] 实现错误处理机制
   - [ ] 编写单元测试
   - [ ] 代码审查重点检查API使用

3. **测试阶段**
   - [ ] 功能测试覆盖所有API调用
   - [ ] 边界条件测试
   - [ ] 错误场景测试
   - [ ] 性能基准测试

### 技术措施
1. **类型安全**
   ```typescript
   // 强制类型检查
   interface ApiResponse<T> {
     data: T
     status: number
     message?: string
   }
   
   // 空值保护
   function safeApiCall<T>(apiCall: () => Promise<T>): Promise<T | null> {
     return apiCall().catch(error => {
       console.error('API call failed:', error)
       return null
     })
   }
   ```

2. **错误处理**
   ```typescript
   // 统一错误处理
   class ApiError extends Error {
     constructor(
       message: string,
       public code: string,
       public details?: any
     ) {
       super(message)
     }
   }
   
   // 降级处理
   async function getWithFallback<T>(
     primary: () => Promise<T>,
     fallback: () => Promise<T>
   ): Promise<T> {
     try {
       return await primary()
     } catch (error) {
       console.warn('Primary API failed, using fallback:', error)
       return await fallback()
     }
   }
   ```

3. **测试策略**
   ```typescript
   // Mock测试
   jest.mock('third-party-lib', () => ({
     api: {
       method: jest.fn()
     }
   }))
   
   // 集成测试
   describe('API Integration', () => {
     it('should handle API errors gracefully', async () => {
       // 测试错误场景
     })
     
     it('should return correct data types', async () => {
       // 测试类型安全
     })
   })
   ```

## 📚 案例研究

### 案例：simple-git库字段映射错误
**问题**：使用`status.working_tree`获取undefined
**根因**：API文档过时，实际字段名为`working_dir`
**解决**：
1. 深入研究库源码
2. 发现正确字段名
3. 更新类型定义
4. 添加空值保护

**经验教训**：
- 不能完全信任文档
- 需要验证API实际行为
- 类型定义很重要

## 🎯 快速参考

### 常见API误用类型
1. **字段名错误**：文档与实际不符
2. **参数顺序错误**：参数位置或类型错误
3. **异步处理错误**：Promise/async-await使用错误
4. **生命周期错误**：调用时机不当
5. **配置错误**：初始化参数错误

### 调试工具
1. **TypeScript编译器**：类型检查
2. **浏览器开发者工具**：网络请求检查
3. **单元测试框架**：行为验证
4. **API文档工具**：如Swagger、Postman

### 应急处理
1. **降级方案**：提供基本功能
2. **错误边界**：防止崩溃
3. **用户提示**：友好的错误信息
4. **日志记录**：便于后续分析

---

**注意**：此模式应在SDD调试流程的"方案设计"阶段使用，配合根因分析和历史检查，确保问题得到系统性解决。