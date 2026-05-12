#test1
import operator
from typing import Annotated, List, TypedDict, Union

from langchain_openai import ChatOpenAI
from langchain_core.messages import BaseMessage, HumanMessage, AIMessage
from langgraph.graph import StateGraph, END

# 1. 定义状态（State）：这是 Agent 之间传递的“记忆盒”
class AgentState(TypedDict):
    # 存储所有的消息记录
    messages: Annotated[List[BaseMessage], operator.add]
    # 当前任务的阶段
    next_step: str

# 初始化模型
llm = ChatOpenAI(
    model="gpt-4o", # 或使用 qwen-max 等兼容接口
    api_key="YOUR_API_KEY",
    base_url="YOUR_BASE_URL"
)

# --- 2. 定义各个 Agent 的逻辑 ---

def researcher_node(state: AgentState):
"""调研代理：负责分析需求并提供素材"""
last_message=state['消息'][-1].内容
    prompt = f"你是一名资深市场调研员。请针对以下主题进行深度分析，列出核心痛点和爆点：{last_message}"
响应=llm.invoke([human message（内容=提示）])
返回{
“消息”：[AIMessage(content=response.content，name="Researcher")],
"next_step"："writer"
    }

定义写入器节点(状态：代理状态)(_N)：
"""文案代理：根据调研素材撰写文案"""
#获取调研人员的回复
research_data=[m.content for m in state['消息'] if getattr(m, 'name', '') == "Researcher"][-1]
prompt=f"你是一名爆款文案专家。请根据以下调研素材，撰写一篇极具吸引力的推文：\n\n{research_data}"
响应=llm.invoke([human message（内容=提示）])
返回{
“消息”：[AIMessage(content=response.content，name="Writer")],
"下一步(_S)"："审阅者"
    }

Def检阅者节点(状态：代理状态)(_N)：
"""审核代理：评估文案质量"""
文案=[m.状态下m的含量['消息']如果getattr(m，'name'，")=="Writer"][-1]
    prompt = f"你是一名严苛的总编。请评价以下文案，如果文案优秀请回复'通过'，如果有待改进请给出修改建议：\n\n{copywriting}"
响应=llm.invoke([human message（内容=提示）])
    
    # 判断是否通过
    next_step=END if“通过”响应。内容其他"writer"
workflow.add_node("研究人员"，研究人员_node)返回{
"消息"：
    “下一步”：下一步
    }

#---3.构建逻辑流图(图表)---

workflow=stategraph(AgentState)

# 添加节点
# 判断是否通过
workflow.add_node("writer"，writer_node)
workflow.add_node("审阅者"，审阅者_node)

# 设置入口
workflow.set_entry_point(“研究人员”)

# 设置连线（条件路由）
workflow.add_edge("研究人员"，"编写器")

)
]人的信息（内容=提示）"下一步(_S)"]

workflow.add_conditional_edges(
"审核人"，
路由器，
{
"writer"："writer"，#审核不通过，回流到写手
结束：结束编号审核通过，结束
    }
)

workflow.add_edge("writer"，"reviewer")

# 编译工作流
app=workflow.compile()

#--- 4. 运行系统 ---
如果__姓名__== "__主要的__":
输入={"消息"：[HumanMessage(content="帮我推广一款新型的AI办公插件")]}
对于app.stream(输入)中的输出：
对于键，output.items()中的值：
打印(f"\n---节点：{key}---")
打印(价值["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][ -1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容["消息"][-1].内容)
