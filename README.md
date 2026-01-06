
<div align="center">

  <img src="assets/icon/responsive_icon.png" alt="Logo" width="100" height="100">

  <h1 align="center">Responsive UI & Layout Architecture</h1>

  <p align="center">
    A technical showcase demonstrating advanced <b>Adaptive Layouts</b> in Flutter using <code>LayoutBuilder</code>, Widget Abstraction, and Constraint analysis.
    <br />
    <br />
    <a href="https://flutter.dev">
      <img src="https://img.shields.io/badge/Flutter-3.x-02569B?style=flat-square&logo=flutter&logoColor=white" alt="Flutter">
    </a>
    <a href="https://dart.dev">
      <img src="https://img.shields.io/badge/Dart-3.x-0175C2?style=flat-square&logo=dart&logoColor=white" alt="Dart">
    </a>
    <img src="https://img.shields.io/badge/Focus-Responsive%20Design-orange?style=flat-square" alt="Focus">
  </p>
</div>

---

## 🧐 Project Overview

This project is not just a UI clone; it is a study in **Responsive Design Principles**. The goal was to build a single application that adapts fluidly across Mobile, Tablet, and Desktop environments without relying on heavy third-party responsive frameworks.

Instead of scaling widgets up, the app utilizes **Layout Branching** to render entirely different architectural structures based on available screen width.

## 📱 Adaptive Behavior Gallery

### 📸 Static Layouts
<div align="center">
  <table>
    <tr>
      <th align="center">Mobile View<br>(< 600px)</th>
      <th align="center">Tablet View<br>(600px - 1100px)</th>
      <th align="center">Desktop View<br>(> 1100px)</th>
    </tr>
    <tr>
      <td align="center">
        <img width="410" height="770" alt="Mobile View" src="https://github.com/user-attachments/assets/ee164766-d6f5-4c24-b49a-a67dc0a78c24" />
        <br />
        <i>Drawer & ListView</i>
      </td>
      <td align="center">
        <img width="652" height="767" alt="Tablet View" src="https://github.com/user-attachments/assets/44c327d6-179e-4399-99c5-28907ec06046" />
        <br />
        <i>Nav Rail & Split View</i>
      </td>
      <td align="center">
        <img width="1260" height="766" alt="Desktop View" src="https://github.com/user-attachments/assets/6eae197d-e288-493f-b148-7a0457524f4e" />
        <br />
        <i>Sidebar & Expanded Grid</i>
      </td>
    </tr>
  </table>
</div>

<br>

### ⏯️ Live Resizing Demo
<div align="center">
  <!-- 
    1. Upload your video to GitHub (drag and drop it into an issue or readme editor).
    2. Copy the link (e.g., https://github.com/user-attachments/assets/...).
    3. Paste it into the src="" below.
  -->
  <video src="https://github.com/user-attachments/assets/b0c7d872-ab69-4b47-bb13-f017e2eab260" width="85%" controls="controls" muted="muted"></video>
  <br/>
  <p><i>Watch the application adapt in real-time as the constraints change.</i></p>
</div>

---

## ⚙️ Technical Implementation

### 1. The `LayoutBuilder` Strategy (Branching)
I utilized the `LayoutBuilder` widget to access the parent constraint's `maxWidth`. This allows the app to make logical decisions on which scaffold structure to return.

*   **Mobile:** Returns a Scaffold with a `BottomNavigationBar` or `Drawer`.
*   **Tablet:** Returns a split-view with a vertical `NavigationRail`.
*   **Desktop:** Returns a wide layout with a permanent sidebar and expanded content areas.

```dart
// Core Logic Snippet
Widget build(BuildContext context) {
  return LayoutBuilder(
    builder: (context, constraints) {
      if (constraints.maxWidth > 1100) {
        return DesktopLayout(); // Separate Widget
      } else if (constraints.maxWidth > 600) {
        return TabletLayout();  // Separate Widget
      } else {
        return MobileLayout();  // Separate Widget
      }
    },
  );
}
```
---

### 2. Widget Abstraction & Reusability
To maintain clean code (DRY Principles), I abstracted UI components that are shared across layouts but behave differently.

*   **Concept:** "Write logic once, render differently."
*   **Example:** A `ProjectCard` widget takes data as a parameter.
    *   In a `ListView` (Mobile), it renders as a compact horizontal tile.
    *   In a `GridView` (Desktop), it expands to use available width, revealing more details.

### 3. Constraint-Based Measurements
Instead of using hardcoded pixel values (`width: 300`), the UI relies on fractional logic and constraint analysis.
*   Used `AspectRatio` to maintain image consistency regardless of screen size.
*   Used `Flexible` and `Expanded` to ensure widgets consume remaining space without causing overflow errors.

---

## 📏 Breakpoint System

The application is tuned to specific width breakpoints to trigger layout changes:

| Device Type | Breakpoint Range | UI Strategy |
|:---|:---|:---|
| **Mobile** | `0px - 600px` | Single Column, Vertical Scroll, Drawer Navigation |
| **Tablet** | `601px - 1100px` | Two Columns (2:1 ratio), Navigation Rail |
| **Desktop** | `1100px +` | Multi-Column (Sidebar + Content + Details), Grid Systems |

---

## 📂 Project Structure

The project is organized to separate the "Responsive Logic" from the "Content Widgets."

```text
lib/
├── responsive/
│   ├── responsive_layout.dart   # The central LayoutBuilder wrapper
│   ├── mobile_body.dart         # Specific mobile implementation
│   ├── tablet_body.dart         # Specific tablet implementation
│   └── desktop_body.dart        # Specific desktop implementation
├── components/                  # Reusable abstracted widgets
│   ├── my_box.dart              # Adaptive container
│   └── my_tile.dart             # Adaptive list tile
├── theme/
│   └── app_theme.dart
└── main.dart
```

---

## 🚀 Key Takeaways & Challenges

*   **Contextless Resizing:** Learned how `LayoutBuilder` differs from `MediaQuery` (LayoutBuilder gives constraints of the *parent*, MediaQuery gives size of the *screen*).
*   **State Preservation:** Handling state when switching between Mobile and Desktop layouts (e.g., ensuring text inputs aren't lost when resizing the window).
*   **Testing:** Manually testing window resizing on Flutter Web/MacOS to ensure zero pixel-overflow errors.

---

## 🛠 Usage

1.  Clone the repo:
    ```sh
    git clone https://github.com/your-username/responsive-project.git
    ```
2.  Run on Chrome or MacOS/Windows to see the resizing in action:
    ```sh
    flutter run -d chrome
    ```
3.  **Resize your browser window** to watch the layout snap between mobile, tablet, and desktop views live.

---
```
