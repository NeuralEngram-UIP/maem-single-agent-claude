# Multi-agent-ebbinghaus-memory-model


## Why This Project Matters

Most AI systems today treat memory as a simple storage and retrieval layer, which limits how naturally agents can adapt over time. MemoryOS introduces a shift from static memory to dynamic cognitive memory, where information has a lifecycle—born, strengthened, weakened, and eventually forgotten.

This approach improves long-term reasoning by ensuring that only relevant and reinforced knowledge influences future decisions. It reduces noise in memory systems, improves retrieval quality, and makes multi-agent systems more realistic and scalable.

Instead of storing everything, MemoryOS focuses on storing what actually matters over time.

# Ebbinghaus Memory Agent

A multi-agent memory system that models human forgetting using the Ebbinghaus
retention curve, with semantic search and SQLite persistence.

## Architecture

```
memory_agent/
├──single_agent 
    ├── agent.py     
    ├── app.py                
    ├── maem_demo.html           # Standalone browser prototype
├── requirements.txt
└── memory_core/
    ├── ebbinghaus.py           # Retention formula: R = e^(-t/S)
    ├── working_memory.py       # Short-term context buffer (deque)
    └── episodic_memory.py      # Long-term SQLite store + semantic search
```

## Key Features

| Feature | Implementation |
|---|---|
| Forgetting curve | `ebbinghaus.compute_retention()` — R = e^(−t/S) |
| Memory decay | `replay_weak()` + `prune_forgotten()` background thread |
| Memory priority | `priority_score()` = retention × importance × log(1 + reviews) |
| Agent learning | `reinforce_memory()` with diminishing returns |
| Multi-agent silos | `user_id` filtering in all retrieval paths |
| Persistence | SQLite WAL mode — survives process restarts |
| Semantic search | `sentence-transformers` all-MiniLM-L6-v2 cosine similarity |
| Context budget | `trim_to_token_limit()` keeps working memory within token limits |

## Alzheimer’s Patient Companion! : An Application

This system can be conceptually used to simulate memory degradation patterns similar to Alzheimer’s disease, where memory retention gradually weakens and recall becomes inconsistent over time.

By modeling controlled memory decay, it becomes possible to study how information loss affects decision-making and recall behavior in cognitive systems.

### Key simulation ideas:
- Gradual reduction in memory retention strength over time  
- Increased likelihood of forgetting rarely accessed information  
- Fragmented recall where partial or related memories are retrieved instead of complete ones  
- Difficulty in forming long-term stable memories without reinforcement  

Such models can help in research-oriented studies of memory degradation patterns and in designing systems that remain robust even under constrained or unreliable memory conditions.