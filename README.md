
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

<div align="center">
  <table>
    <tr>
      <th align="center">Mobile View<br>(< 600px)</th>
      <th align="center">Tablet View<br>(600px - 1100px)</th>
      <th align="center">Desktop View<br>(> 1100px)</th>
    </tr>
    <tr>
      <!-- REPLACE WITH YOUR IMAGES -->
      <td align="center">
        <img src="https://via.placeholder.com/200x400.png?text=Mobile" width="160" alt="Mobile View">
        <br />
        <i>Drawer & ListView</i>
      </td>
      <td align="center">
        <img src="https://via.placeholder.com/300x400.png?text=Tablet" width="240" alt="Tablet View">
        <br />
        <i>Nav Rail & Split View</i>
      </td>
      <td align="center">
        <img src="https://via.placeholder.com/500x350.png?text=Desktop" width="350" alt="Desktop View">
        <br />
        <i>Sidebar & Expanded Grid</i>
      </td>
    </tr>
  </table>
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
