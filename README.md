# dfl_proj

Decision-Focused Learning（决策导向学习）与端到端 Predict-and-Optimize（预测—优化联合学习）的调研和模型实现项目，重点关注储能运行。

## 当前状态

已建立研究文档、工程约定、uv 管理的 Python 3.11.9 虚拟环境和 Git 仓库（`main` 分支）。当前为非打包研究项目，尚未安装模型依赖或实现训练模型。

## 环境使用

```bash
uv sync --locked
env -u PYTHONPATH uv run python --version
```

解释器固定为 `.python-version` 中的 Python 3.11.9，环境位于项目根目录 `.venv/`。提交 `pyproject.toml`、`.python-version` 和 `uv.lock`，不提交虚拟环境、密钥、缓存及本地数据／实验结果。后续依赖统一使用 `uv add`。

## 文档

- [DFL 与储能预测—优化联合训练调研](docs/2026-09-13-dfl-predict-and-optimize.html)：12 个章节，涵盖数学模型、方法分类、多阶段训练、论文、代码核查、场景适配与验证路线。自包含 HTML，直接在浏览器打开即可，支持目录高亮与打印。
- [来源索引](docs/references/sources.json)：调研引用 URL 的结构化索引。
- [工程规范](AGENTS.md)：目录、环境、科学协议与产物要求。

## 后续实现约定

按实际功能创建 `src/dfl_proj/`、`tests/`、`configs/`、`scripts/`。Python 统一使用本项目根目录 `.venv` 与 `uv`，模型依赖待兼容性 spike 后选定；环境已建立不代表优化求解器或训练模型通过兼容性验证。数据与实验结果分别归入 `data/`、`results/`。

主场景已确定：预测未来一天 96 点负荷（15 分钟平均功率），将已知固定峰谷平电价作为优化输入，输出次日完整 96 点储能充放电功率计划。净功率正值表示放电、负值表示充电，同时保留两条分开功率序列及 97 个边界电量状态。费率及时段表、设备参数、反送电／并网限额、需量费和安全执行规则待确认；日内滚动重优化不是默认交付。论文中的电价预测与报价实验仅作参考，不能代替本地实测。
