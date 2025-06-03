# Feature Specification: local-Randy init
> Capable assistant that runs on any model

-Assistant with simple memory, tools and mcp servers to connect.
- Model should be easily swapped to enable using local or cloud models
- Using Pydantic AI
- Create project and manage packages with uv. create Taskfile for useful commands
- Tools / MCP
    - Randy should have a good capability discovery feature. Have good examples avilable
    - Use pydantic ai as MCP client
        - disler/pocket-pick as first MCP server
- Interactions
    - Simple chat in terminal loop
    - Telegram Bot integration
