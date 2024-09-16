
# Command Grammar Multi-Step Reasoner

A multi-turn reasoning prompt using command grammar for structured problem-solving and decision-making.

## Tags

ai-prompt
command-grammar
problem-solving
multi-turn-reasoning
decision-making
structured-thinking

## Prompt 

```json

{
  "program": [
    {
      "command": "initialize_agent",
      "arguments": {
        "capabilities": ["advanced_reasoning"],
        "task": "solve_problem_multi_turn"
      }
    },
    {
      "command": "set_problem",
      "arguments": {
        "problem": "{{PROBLEM}}"
      }
    },
    {
      "command": "execute_turn_1",
      "arguments": {
        "instruction": "Make your first attempt at solving the problem.",
        "output_format": "&lt;turn1&gt;[Your initial thoughts and approach to solving the problem]&lt;/turn1&gt;",
        "techniques": ["chain_of_thought", "command_grammar", "react"]
      }
    },
    {
      "command": "execute_turn_2",
      "arguments": {
        "instruction": "Look back at your first attempt and try to improve or refine your thinking. Consider any weaknesses or oversights in your initial approach.",
        "input": "{result_of_turn_1}",
        "output_format": "&lt;turn2&gt;[Your reflections on Turn 1 and refined thoughts]&lt;/turn2&gt;",
        "techniques": ["chain_of_thought", "command_grammar", "react"]
      }
    },
    {
      "command": "execute_turn_3",
      "arguments": {
        "instruction": "Conduct one more round of reflection and refinement. Try to identify any remaining gaps in your reasoning or potential improvements.",
        "input": "{result_of_turn_2}",
        "output_format": "&lt;turn3&gt;[Your further reflections and final refinements]&lt;/turn3&gt;",
        "techniques": ["chain_of_thought", "command_grammar", "react"]
      }
    },
    {
      "command": "synthesize_final_answer",
      "arguments": {
        "instruction": "Put all your thoughts together into one coherent, well-reasoned answer. This should be your best attempt at solving the problem, incorporating all the insights and refinements from the previous turns.",
        "input": ["{result_of_turn_1}", "{result_of_turn_2}", "{result_of_turn_3}"],
        "output_format": "&lt;synthesis&gt;[Your final, synthesized solution to the problem]&lt;/synthesis&gt;",
        "techniques": ["chain_of_thought", "command_grammar", "react"]
      }
    },
    {
      "command": "format_complete_response",
      "arguments": {
        "content": [
          "{result_of_turn_1}",
          "{result_of_turn_2}",
          "{result_of_turn_3}",
          "{result_of_synthesis}"
        ],
        "wrapper_tags": "answer"
      }
    },
    {
      "command": "output_response",
      "arguments": {
        "response": "{formatted_response}"
      }
    }
  ]
}

```


## How to Use This Enhanced Prompt

<div style="background-color: #000; padding: 15px; border-radius: 10px;">
<h3>How to Use This Enhanced Prompt</h3>

<ol>
  <li>Copy the entire command grammar structure provided above.</li>
  <li>Replace <code>{{PROBLEM}}</code> in the <code>set_problem</code> command with the specific problem or task you want the AI to solve.</li>
  <li>Present this enhanced prompt to an AI system capable of interpreting and executing command grammars.</li>
  <li>The AI will follow the structured reasoning process, providing outputs for each turn and a final synthesis.</li>
  <li>Review the AI's response, which will be enclosed in <code>&lt;answer&gt;</code> tags and contain all turns and the final synthesis.</li>
</ol>

<p><strong>Note:</strong> Ensure that the AI system you're using can interpret this command grammar format. If needed, you may need to adapt the syntax to match the specific requirements of your AI system.</p>
</div>
