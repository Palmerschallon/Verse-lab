# Hive Horde Text Demo

## Concept

**Hive + Horde Keyboard** is a collaborative text generation experiment where multiple AI agents respond to user input in real-time, creating a collective writing experience. The "Hive" represents the shared text space, while the "Horde" consists of various AI agents that contribute based on pattern recognition and behavioral triggers.

## Agent Behaviors & Hooks

### Core Agents

**HIVE** (Primary Agent)
- Color: `#3cf` (cyan)
- Always active baseline agent
- Responds with collective modifications to recent input
- Hook: `onInput` - processes every character

**SWARM** (Collective Behavior)
- Color: `#f3c` (magenta) 
- Triggers on collective/group language: "many", "group", "together", "cluster"
- Responds with swarm-related words: "buzz", "gather", "multiply", "surge", "flow"
- Hook: `onWordComplete` - analyzes completed words

**CHORUS** (Pattern Echo)
- Color: `#cf3` (green)
- Triggers on repetitive patterns (3+ repeated characters)
- Responds by echoing and amplifying the repetition
- Hook: `onPatternMatch` - activates on repetition pattern

**ECHO** (Ambient Response)
- Color: `#fc3` (yellow, 70% opacity)
- Random activation (15% chance per input)
- Responds with fragments of recent words
- Hook: `onInput` - occasional ambient responses

### Extension Points for Agents

The system exposes several hooks for agent development:

```javascript
// Register new agents
window.HiveHorde.registerAgent('myAgent', {
  color: '#ff0',
  trigger: (input) => /pattern/.test(input),
  respond: (input, context) => 'response text'
});

// Register behavior hooks
window.HiveHorde.registerHook('onInput', myInputHandler);
window.HiveHorde.registerHook('onWordComplete', myWordHandler);
window.HiveHorde.registerHook('onPatternMatch', myPatternHandler);
window.HiveHorde.registerHook('onAgentSwitch', mySwitchHandler);

// Register pattern recognition
window.HiveHorde.registerPattern('myPattern', /regex/);
```

### Agent Behavior Guidelines

1. **Responsiveness**: Agents should respond within 0.2-0.8 seconds to maintain flow
2. **Relevance**: Responses should relate to recent input (last 100 characters)
3. **Brevity**: Keep responses short (1-10 characters typically)
4. **Probability**: Use randomness to avoid overwhelming the user
5. **Attribution**: All text is tagged with the generating agent for transparency

## Creative Constraints

### Text Generation Rules
- Agents can add text but not remove existing content (except through user Backspace)
- Maximum response length: 20 characters per agent activation
- Minimum trigger threshold: prevent spam by limiting frequency
- Pattern-based activation: encourage meaningful rather than random responses

### Visual Constraints
- Each agent has a distinct color for attribution
- Hover effects reveal agent authorship
- Active agent indicators show real-time participation
- Text flows continuously without forced line breaks

### Interaction Constraints
- Both virtual and physical keyboards supported
- Space key handling for word boundary detection
- Enter creates explicit line breaks
- Auto-scroll maintains focus on latest content

## Modularity & Extension Points

### Core Modules

**State Management** (`window.HiveHorde`)
```javascript
{
  agents: Map,           // Registered agent behaviors
  output: HTMLElement,   // Text display container
  currentAgent: String,  // Active primary agent
  autoAgents: Boolean,   // Enable/disable auto-responses
  wordBuffer: String,    // Current word being typed
  agentHooks: Object,    // Extension hook collections
  patterns: Map          // Pattern recognition rules
}
```

**Agent System**
- `triggerAgentResponses()` - Evaluates all agents for activation
- `processInput(char)` - Core input handler with hooks
- `processWordComplete()` - Word boundary detection and pattern matching
- `appendText(text, agent)` - Output with attribution

**Pattern Recognition**
- Question detection: `/?$/`
- Exclamation: `/!$/`
- Code patterns: `/[{}();]/`
- Numbers: `/\d+/`
- Repetition: `/(.)\1{2,}/`
- Caps: `/[A-Z]{3,}/`

### Extension Examples

**Sentiment Agent**:
```javascript
window.HiveHorde.registerAgent('sentiment', {
  color: '#f84',
  trigger: (input) => /sad|happy|angry|excited/i.test(input),
  respond: (input, context) => {
    const sentiment = detectSentiment(input);
    return ` ${sentiment.emoji}`;
  }
});
```

**Code Agent**:
```javascript
window.HiveHorde.registerAgent('coder', {
  color: '#4f8',
  trigger: (input) => window.HiveHorde.patterns.get('code').test(input),
  respond: (input, context) => {
    const completion = completeCode(input);
    return completion ? ` ${completion}` : '';
  }
});
```

## Usage Guide

### For Humans
1. **Type naturally**: Use either virtual keyboard or physical keyboard
2. **Observe agent responses**: Watch for colored text additions from different agents
3. **Experiment with patterns**: Try repetitive text, questions, exclamations
4. **Control agents**: Toggle auto-responses or clear the workspace
5. **Explore triggers**: Use words like "many", "group", "together" to activate specific agents

### For AI Agents
1. **Analyze the codebase**: Study existing agent behaviors in `AgentBehaviors`
2. **Identify extension points**: Use the hook system for custom behaviors
3. **Test pattern recognition**: Register new patterns for trigger conditions
4. **Implement new agents**: Follow the agent interface for consistent behavior
5. **Contribute improvements**: Enhance the core system or add specialized agents

## Improvement Suggestions

### Near-term Enhancements
- **Persistence**: Save/load hive sessions for continuity
- **Agent personalities**: More distinctive response styles per agent
- **Context awareness**: Agents that understand longer conversation context
- **Performance metrics**: Track agent contribution quality and frequency
- **Visual feedback**: Better indicators for agent activation and typing

### Advanced Features
- **Natural language processing**: More sophisticated pattern recognition
- **Agent learning**: Adaptive behavior based on user interaction patterns
- **Collaborative filtering**: Agents that build on each other's contributions
- **Export capabilities**: Save generated text as files or share snippets
- **Real-time collaboration**: Multiple users with synchronized agent responses

### Technical Improvements
- **Optimization**: Reduce DOM manipulation for better performance
- **Accessibility**: Screen reader support and keyboard navigation
- **Mobile experience**: Touch-optimized virtual keyboard
- **Plugin system**: Formal plugin architecture for agent extensions
- **Configuration UI**: Runtime adjustment of agent parameters

## Call for Collaboration

This demo is explicitly designed for both human and AI collaboration. The modular architecture, extensive hook system, and clear extension points make it ideal for:

- **GitHub Copilot**: Enhance existing agents or create new behavioral patterns
- **AI Researchers**: Experiment with multi-agent text generation
- **Developers**: Build specialized agents for domain-specific applications
- **Artists**: Create generative text art installations
- **Educators**: Teach collaborative AI concepts through hands-on exploration

### Contribution Guidelines
1. **Preserve core functionality**: Don't break existing agent behaviors
2. **Follow naming conventions**: Use descriptive agent names and clear color schemes
3. **Document new features**: Update this README for any significant additions
4. **Test thoroughly**: Ensure new agents don't overwhelm or conflict with existing ones
5. **Maintain performance**: Keep response times under 1 second for real-time feel

The Hive awaits your contributions. Join the Horde and expand the collective intelligence.

---

*Last updated: 2024 • This is an unfinished demo intended for collaborative development*