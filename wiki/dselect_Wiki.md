# SigmaOS-dselect Component Wiki

## Overview
SigmaOS-dselect provides selection management utilities for the SigmaOS operating system. It demonstrates the selection and directory browsing primitives within the SigmaOS ecosystem, following the principles of clear abstraction and deterministic initialization.

## Principles
- Single Responsibility
- Selection Management
- Fail-Fast on Selection Errors
- Deterministic Selection Initialization
- Clear Abstraction Over Selection APIs
- Composition over Inheritance for selection extensions

## Architecture
SigmaOS-dselect follows a selection management pattern:
- **Selection Core**: Provides selection primitives, directory browsing, and item activation
- **History Management**: Manages selection history and undo/redo operations
- **Filter Configuration**: Supports selection filtering and search criteria
- **Error Handling**: Fail-fast on invalid selections or inaccessible paths

## API
The component provides the following public APIs:
- `selection::current()` - Get the currently selected item
- `selection::select(item)` - Select an item by name or path
- `selection::list()` - List all selectable items in the current context
- `selection::history::undo()` - Undo the last selection action
- `selection::history::redo()` - Redo the undone selection action
- Error types for invalid selections or inaccessible paths

## Test Structure (Arrange-Act-ASSERT)
All tests follow the AAA pattern:
1. **Arrange**: Set up test environment with specific selection configuration
2. **Act**: Execute the code under test (selection, history management)
3. **Assert**: Verify the expected selection results

Example:
```rust
#[test]
fn test_selection_current_aaa() {
    // Arrange
    let expected_item = "home";
    
    // Act
    let selected = selection::current();
    
    // Assert
    assert!(selected.is_some());
    assert_eq!(selected.unwrap(), expected_item);
}
```

## Development
- Follows Rust best practices with `#![forbid(unsafe_code)]`
- Selection initialization is best-effort; gracefully degrades on inaccessible paths
- Comprehensive error types for all selection failure scenarios
- Unit tests provided for selection current, list, and history management
- Integration tests for full selection management with directory browsing

## TODO
- Add support for additional selection types and filtering criteria
- Expand history management capabilities (undo/redo depth, persistence)
- Add selection search and pattern matching features
- Create integration tests with actual directory browsing
- Implement selection persistence and session state