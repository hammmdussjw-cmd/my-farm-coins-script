# my-farm-coins-script
Update ONLY the reset execution when "Auto Reset (40 Max)" triggers at `coins >= 40` so it uses a fallback sequence (A -> B -> C -> D) until the character actually dies.

Apply ONLY this A-B-C-D reset sequence when `coins >= 40` and the character is alive:
1. Before running the sequence, immediately stop/cancel any active coin movement and zero out `AssemblyLinearVelocity`.
2. Run a short reset sequence checking if `Humanoid.Health <= 0` or `Humanoid:GetState() == Enum.HumanoidStateType.Dead` after each step (with a tiny ~0.12s check interval):
   - Step A: Set `Humanoid.Health = 0`.
   - Step B: If still alive, call `Humanoid:ChangeState(Enum.HumanoidStateType.Dead)`.
   - Step C: If still alive, call `Character:BreakJoints()`.
   - Step D: If still alive, destroy/clear character parts (`HumanoidRootPart:Destroy()` / `Character:BreakJoints()` again) as the final fallback.

DO NOT modify any other code, UI sizing (`UDim2.new(0, 260, 0, 185)`), title ("🔪 djdjdhr99 | Coins Farm 🔪"), top-center `🔪` toggle, red `X` button, the 4 toggles, safe speed cap/pacing delay, automatic Noclip while farming, or dead/lobby/spectate pause. Return the complete, unabbreviated script.