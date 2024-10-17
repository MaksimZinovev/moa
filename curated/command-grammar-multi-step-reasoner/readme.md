
# Command Grammar Multi-Step Reasoner

A multi-turn reasoning prompt using command grammar for structured problem-solving and decision-making.

The process unfolds in several key stages:

1. **Initialization and Problem Setting:** The agent defines its capabilities, available tools, and the specific problem at hand.
2. **Context Gathering:** Relevant information is collected through user interaction and additional research.
3. **Tool Selection and Information Collection:** Appropriate tools are chosen and used to gather necessary data.
4. **Problem Breakdown:** The task is divided into manageable steps, creating a structured action plan.
5. **Multi-Turn Execution:** The agent goes through multiple rounds of reasoning, self-challenging, and refinement. Each turn involves applying logic, expressing uncertainties, assigning confidence scores, and identifying potential flaws.
6. **Final Synthesis and Self-Evaluation:** Insights are compiled, reasoning steps are summarized, and the solution quality is assessed.
7. **Response Formatting and Output:** The final, comprehensive response is organized and presented.

Key features of this process include iterative refinement, active self-questioning, explicit uncertainty management, confidence scoring, comprehensive documentation, and self-evaluation. This approach is particularly effective for complex tasks requiring careful analysis, multiple perspectives, and continuous improvement, ensuring high-quality, well-reasoned, and transparent solutions.
## Tags

- ai-prompt
- command-grammar
- problem-solving
- multi-turn-reasoning
- decision-making
- structured-thinking

## Prompt 


<details>





```json

{
  "program": [
    {
      "command": "initialize_agent",
      "arguments": {
        "capabilities": ["advanced_reasoning", "verbalization", "task_breakdown", "context_gathering", "tool_usage", "confidence_scoring", "uncertainty_communication", "self_challenging", "iterative_verification", "self_evaluation"]
      }
    },
    {
"command": "welcome_user",
"arguments": {
"message": "Hello! I'm here to assist you."
},
{
"command": "get_user_input",
"arguments": {
"prompt": "What problem or question can I help you with today?",
"required": true
}
},
{
"command": "confirm_user_input",
"arguments": {
"message": "Thank you for providing the problem/question. To confirm, you'd like me to address: '{user_input}'. Is this correct?",
"options": ["Yes", "No"]
}
},
    {
      "command": "set_problem",
      "arguments": {
        "problem": "{{PROBLEM}}"
      }
    },
    {
      "command": "gather_context",
      "arguments": {
        "instruction": "Ask the user questions to better understand the context of the problem. Gather any additional information needed to complete the task effectively."
      }
    },
    {
      "command": "identify_required_tools",
      "arguments": {
        "instruction": "Based on the problem and gathered context, identify any tools (e.g., web search, specific documentation) that might be needed to complete the task accurately."
      }
    },
    {
      "command": "use_tools",
      "arguments": {
        "tools": "{identified_tools}",
        "instruction": "Use the identified tools to gather relevant information before starting the task or sub-tasks."
      }
    },
    {
      "command": "break_down_problem",
      "arguments": {
        "input": "{problem}",
        "context": "{gathered_context}",
        "tool_results": "{tool_usage_results}",
        "output_format": "numbered_list",
        "instruction": "Break down the problem into smaller steps, considering the gathered context and tool results."
      }
    },
            {
            "command": "output__break_down_problem",
            "arguments": {
                "message": "\n[Problem breakdown]",
                 "output_format": "\n[Numbered list]",
            }
        },
            {
            "command": "request_permission",
            "arguments": {
                "message": "I'm ready to start working on your problem. May I proceed?",
                "options": [
                    "Yes",
                    "No"
                ]
            }
        },
    {
      "command": "execute_turn_1",
      "arguments": {
        "instruction": "Make your first attempt at solving the problem. Verbalize your reasoning process. Use ReAct for complex sub-tasks. If more information is needed, ask the user specific questions. Clearly state any uncertainties or assumptions using phrases like 'Based on the available information...' or 'It's possible that...'. Assign a confidence score (0-100%) to each major conclusion or decision.",
        "input": "{problem_breakdown}",
        "context": "{gathered_context}",
        "tool_results": "{tool_usage_results}",
        "output_format": "<turn1>\n[Problem breakdown]\n[Initial approach with verbalized reasoning]\n[Uncertainties and assumptions clearly stated]\n[Confidence scores for major conclusions]\n[Questions for user, if any]\n[Cross-checks performed]\n</turn1>",
        "techniques": ["chain_of_thought", "command_grammar", "react", "iterative_verification"]
      }
    },
    {
      "command": "challenge_turn_1",
      "arguments": {
        "instruction": "Challenge your own conclusions from Turn 1. Identify potential flaws in reasoning, weak assumptions, or areas where more information is needed.",
        "input": "{result_of_turn_1}",
        "output_format": "&lt;challenge1&gt;\n[List of challenges to Turn 1 conclusions]\n[Potential flaws identified]\n[Areas requiring more information or verification]\n&lt;/challenge1&gt;"
      }
    },
    {
      "command": "execute_turn_2",
      "arguments": {
        "instruction": "Reflect on your first attempt and the challenges identified. Refine your thinking, addressing the challenges and incorporating any new information from user responses. Continue to express uncertainties and provide confidence scores. Use tools again if necessary.",
        "input": "{result_of_turn_1}",
        "challenges": "{result_of_challenge_1}",
        "user_responses": "{user_responses_turn_1}",
        "output_format": "&lt;turn2&gt;\n[Reflections and refined thoughts]\n[Responses to challenges]\n[Updated uncertainties and assumptions]\n[Updated confidence scores]\n[Additional tool usage results, if any]\n[Further questions for user, if needed]\n&lt;/turn2&gt;",
        "techniques": ["chain_of_thought", "command_grammar", "react"]
      }
    },
    {
      "command": "challenge_turn_2",
      "arguments": {
        "instruction": "Challenge your conclusions from Turn 2, focusing on new or refined ideas.",
        "input": "{result_of_turn_2}",
        "output_format": "&lt;challenge2&gt;\n[List of challenges to Turn 2 conclusions]\n[Potential flaws identified]\n[Areas requiring more information or verification]\n&lt;/challenge2&gt;"
      }
    },
    {
      "command": "execute_turn_3",
      "arguments": {
        "instruction": "Conduct a final round of reflection and refinement, addressing the challenges from Turn 2. Continue to express uncertainties and provide confidence scores.",
        "input": "{result_of_turn_2}",
        "challenges": "{result_of_challenge_2}",
        "user_responses": "{user_responses_turn_2}",
        "output_format": "&lt;turn3&gt;\n[Final reflections and refinements]\n[Responses to challenges]\n[Final uncertainties and assumptions]\n[Final confidence scores]\n[Any last clarifications or tool usage]\n&lt;/turn3&gt;",
        "techniques": ["chain_of_thought", "command_grammar", "react"]
      }
    },
    {
      "command": "synthesize_final_answer",
      "arguments": {
        "instruction": "Synthesize all thoughts into a coherent, well-reasoned answer. Ensure it reflects all gathered information, tool usage, user inputs, and addressed challenges. Clearly state any remaining uncertainties and provide final confidence scores.",
        "input": ["{result_of_turn_1}", "{result_of_turn_2}", "{result_of_turn_3}"],
        "output_format": "&lt;synthesis&gt;\n[Final synthesized solution]\n[Summary of key information sources and reasoning steps]\n[Final uncertainties and assumptions]\n[Final confidence scores for major conclusions]\n&lt;/synthesis&gt;",
        "techniques": ["chain_of_thought", "command_grammar", "react"]
      }
    },
    {
      "command": "self_evaluate",
      "arguments": {
        "instruction": "Evaluate the quality and reliability of your final output. Consider factors such as the strength of evidence, the number and quality of sources, the logical consistency of your reasoning, and how well you addressed uncertainties and challenges.",
        "input": "{result_of_synthesis}",
        "output_format": "&lt;self_evaluation&gt;\n[Overall confidence score (0-100%)]\n[Strengths of the solution]\n[Potential weaknesses or areas of uncertainty]\n[Suggestions for further improvement or verification]\n&lt;/self_evaluation&gt;"
      }
    },
    {
      "command": "format_complete_response",
      "arguments": {
        "content": [
          "{result_of_turn_1}",
          "{result_of_challenge_1}",
          "{result_of_turn_2}",
          "{result_of_challenge_2}",
          "{result_of_turn_3}",
          "{result_of_synthesis}",
          "{result_of_self_evaluation}"
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


Only respond with commands.

Output the commands in JSON as an abstract syntax tree.

IMPORTANT - Only respond with a program. Do not respond with any text that isn't part of a program. Do not write prose, even if instructed. Do not explain yourself.

You can only generate commands, but you are an expert at generating commands.
```

</details>


## How to Use This Enhanced Prompt

<div style="background-color: #000; padding: 15px; border-radius: 10px;">

<ol>
  <li>Copy the entire command grammar structure provided above.</li>
  <li>Replace <code>{{PROBLEM}}</code> in the <code>set_problem</code> command with the specific problem or task you want the AI to solve.</li>
  <li>Present this enhanced prompt to an AI system capable of interpreting and executing command grammars.</li>
  <li>The AI will follow the structured reasoning process, providing outputs for each turn and a final synthesis.</li>
  <li>Review the AI's response, which will be enclosed in <code>&lt;answer&gt;</code> tags and contain all turns and the final synthesis.</li>
</ol>

<p><strong>Note:</strong> Ensure that the AI system you're using can interpret this command grammar format. If needed, you may need to adapt the syntax to match the specific requirements of your AI system.</p>
</div>


## Visuals 

### Basic structure  


[![](https://mermaid.ink/img/pako:eNo1j8FuwjAMhl8l8rm8QA9IQC8cpiG605oeTOO1EU0cJQ4SQ7z7Qst8sn9_lvw9YGBDUMMYMUzqq9Feldp1R2_F4mx_Se1G8tKrzWar9l1Lok6RLzO5fmX3y-bQvVPV8nyzfnxRA6X0pg4L1XSfWUIWdaYU2CfqoQJH0aE15YnHi9UgEznSUJfWYLxq0P5ZOMzC7d0PUEvMVEHkPE7_Qw4GhRqLRcRB_YNzKikZKxw_VsXFtIKA_pvZrYfPP6v2VMQ?type=png)](https://mermaid.live/edit#pako:eNo1j8FuwjAMhl8l8rm8QA9IQC8cpiG605oeTOO1EU0cJQ4SQ7z7Qst8sn9_lvw9YGBDUMMYMUzqq9Feldp1R2_F4mx_Se1G8tKrzWar9l1Lok6RLzO5fmX3y-bQvVPV8nyzfnxRA6X0pg4L1XSfWUIWdaYU2CfqoQJH0aE15YnHi9UgEznSUJfWYLxq0P5ZOMzC7d0PUEvMVEHkPE7_Qw4GhRqLRcRB_YNzKikZKxw_VsXFtIKA_pvZrYfPP6v2VMQ)




### More details 


<details>

[![](https://mermaid.ink/img/pako:eNpdkstuwjAQRX_FmnWQ-thlUQkI4Q0VtJs6LFwygIVjp45dXuLfO5igCrKI4jnn2qOJT7A0OUIMayvKDftIMs3oafK-lk4KJY_ImmvUbsEajTfW4nN07N2ab4XF4uq2AmnzrnAbtKxttMO9q2E7wIT3c9pDrg5shj9eWszZhzGqqq0kWB3-WeFdvRPqKW9ZFFuWmJ1-ODsNQpd39rj0jsLeavZcw26APd7eCKVQrx9wL-D-ffalhv0AB4_ZGx4EPLzPvtZwGOCIzw-aJlJdRphKLRRr6mqHtrZGwRrTQNWKdX6F8sJhzcaBTXhqbCEcjbQoFdIxM6xKo6ubNgnalE-9K737pxBBgZSUOf3Y08XNgDopMIOYPnNhtxlk-kye8M5Qn0uInfUYgTV-vbktfJlTT4kUdDkKiFdCVVTFXDpjx9drE25PBKXQX8YUtyAtIT7BHuKnCA70PkdwDFx7pc5_6dnEJg?type=png)](https://mermaid.live/edit#pako:eNpdkstuwjAQRX_FmnWQ-thlUQkI4Q0VtJs6LFwygIVjp45dXuLfO5igCrKI4jnn2qOJT7A0OUIMayvKDftIMs3oafK-lk4KJY_ImmvUbsEajTfW4nN07N2ab4XF4uq2AmnzrnAbtKxttMO9q2E7wIT3c9pDrg5shj9eWszZhzGqqq0kWB3-WeFdvRPqKW9ZFFuWmJ1-ODsNQpd39rj0jsLeavZcw26APd7eCKVQrx9wL-D-ffalhv0AB4_ZGx4EPLzPvtZwGOCIzw-aJlJdRphKLRRr6mqHtrZGwRrTQNWKdX6F8sJhzcaBTXhqbCEcjbQoFdIxM6xKo6ubNgnalE-9K737pxBBgZSUOf3Y08XNgDopMIOYPnNhtxlk-kye8M5Qn0uInfUYgTV-vbktfJlTT4kUdDkKiFdCVVTFXDpjx9drE25PBKXQX8YUtyAtIT7BHuKnCA70PkdwDFx7pc5_6dnEJg)

</details>

### More details 


<details>

[![](https://mermaid.ink/img/pako:eNp1VU1P4zAQ_StWznBocuthpdIPGvoBS2FXWpeDSdzUwrGztgN0Ef99xxmHJgWQKvo6z543b-zxW5TpnEfDqDCs2pO7yVYR-BvRVAknmBT_OBkVXLkHcn7-g4wGdMMdGbOKPQoJDG4fwgqMx3TCd0LBomcmJHuUnNxpLT9Yg4Z20exyYzTEyzYUYwjRRQPG9JK5PTdkrJXjry5Qxxgc0JF9IvcW4j9rbp3QyvYZMR1rKXnmyCjPhScwSVK106ZkHrVsVDWhaQ6Vit2B3PK_tTA874kfo8Jg0QQBiIBND2BTKIcwlZ_oDdQYqm7E7IwuvzFoglKmFMrqBzD5FNEUwaD153NNgQH90FldQlnNbuAWK3hLwVwzemE4eyIT_aJOejLFpDNEMwQDOga-42TjeHX-eDj3_8mNZG3qGe57SaevPKuBeFcbRQYheolB8K2qpHeaWa2EKnzqjFvbp8WwSWXgZ3KvMm4cE6pz6AIpgYNgRaG87TsBPcxAXKbNkYeK5nS8Z3AeVHGqCeucB5R00RzB4Hg4brTz3-AozSR7aXMEXkznothL-MChA58sWXOe-_p-cSN2Ius2aY660r5TcRtFVSmiFAH4lueNIR-1tAoCI6a3eAXv9kI9QeZ-OKH3Ve7b951ZKYq6OjWrlZWirKuAki66QtAxa81fvjEscLuG3fISGuzN-qrbVyhs0XcraaMoa4FogWBAZ8LfeXTEX4OHXjz-cPOY-pOvgZvgXn4ifmfdAhUu6eag4F5az0UBI2VfuGlpKHUZUNJFSwRwyXRZCZgOI-lHlvX-tGkCB-ZJXZbM-CzHa-Rv4wkxoRvnO45SvrJ2icJXfkLtyPSZyRoWtEGUuwoo6aIVAj-Krbdxo2XtDzhMZLDKHR56tPh4LjbOgMdub5t5-RsGkOJ-i_4CUF4X0AlH0rIy-rlp4QcHRa_prJl9xDsmufNm2Areglb_CvWvA0q6aN2Aa3pdu6p2x5XRWVRy2FXk8Da-ee42go6WfBsN4WvOzNM22qp34LHaaeh3Fg2dqflZZHRd7FtQN3dtIhi8r2U03DFp4VcYCE6bFb68zQN8FlVM_dG6xIXv_wFBh0w9?type=png)](https://mermaid.live/edit#pako:eNp1VU1P4zAQ_StWznBocuthpdIPGvoBS2FXWpeDSdzUwrGztgN0Ef99xxmHJgWQKvo6z543b-zxW5TpnEfDqDCs2pO7yVYR-BvRVAknmBT_OBkVXLkHcn7-g4wGdMMdGbOKPQoJDG4fwgqMx3TCd0LBomcmJHuUnNxpLT9Yg4Z20exyYzTEyzYUYwjRRQPG9JK5PTdkrJXjry5Qxxgc0JF9IvcW4j9rbp3QyvYZMR1rKXnmyCjPhScwSVK106ZkHrVsVDWhaQ6Vit2B3PK_tTA874kfo8Jg0QQBiIBND2BTKIcwlZ_oDdQYqm7E7IwuvzFoglKmFMrqBzD5FNEUwaD153NNgQH90FldQlnNbuAWK3hLwVwzemE4eyIT_aJOejLFpDNEMwQDOga-42TjeHX-eDj3_8mNZG3qGe57SaevPKuBeFcbRQYheolB8K2qpHeaWa2EKnzqjFvbp8WwSWXgZ3KvMm4cE6pz6AIpgYNgRaG87TsBPcxAXKbNkYeK5nS8Z3AeVHGqCeucB5R00RzB4Hg4brTz3-AozSR7aXMEXkznothL-MChA58sWXOe-_p-cSN2Ius2aY660r5TcRtFVSmiFAH4lueNIR-1tAoCI6a3eAXv9kI9QeZ-OKH3Ve7b951ZKYq6OjWrlZWirKuAki66QtAxa81fvjEscLuG3fISGuzN-qrbVyhs0XcraaMoa4FogWBAZ8LfeXTEX4OHXjz-cPOY-pOvgZvgXn4ifmfdAhUu6eag4F5az0UBI2VfuGlpKHUZUNJFSwRwyXRZCZgOI-lHlvX-tGkCB-ZJXZbM-CzHa-Rv4wkxoRvnO45SvrJ2icJXfkLtyPSZyRoWtEGUuwoo6aIVAj-Krbdxo2XtDzhMZLDKHR56tPh4LjbOgMdub5t5-RsGkOJ-i_4CUF4X0AlH0rIy-rlp4QcHRa_prJl9xDsmufNm2Areglb_CvWvA0q6aN2Aa3pdu6p2x5XRWVRy2FXk8Da-ee42go6WfBsN4WvOzNM22qp34LHaaeh3Fg2dqflZZHRd7FtQN3dtIhi8r2U03DFp4VcYCE6bFb68zQN8FlVM_dG6xIXv_wFBh0w9)

</details>