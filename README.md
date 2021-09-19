// Want to support my work 😎? https://buymeacoffee.com/vandad

```dart
import 'package:flutter/material.dart';
import 'dart:math' show pi;

class NosePainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final width = size.width * 0.1;
    final height = width * 4.0;

    final paint = Paint()
      ..color = Colors.green[900]!
      ..style = PaintingStyle.fill;

    final top = size.height / 2.8;
    final centerX = size.width / 2.0;

    final path = Path();

    path.moveTo(centerX - (width / 2.0), top);
    path.lineTo(centerX + (width / 2.0), top);
    path.lineTo(centerX, top + height);
    path.close();

    canvas.drawPath(
      path,
      paint,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}

class BellyPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final bellyWidth = size.width * 0.6;
    final bellyHeight = bellyWidth / 2.0;

    final centerY = size.height - (bellyHeight / 1.6);
    final paint = Paint()..color = Colors.white;

    final centerX = size.width / 2.0;

    final rect = Rect.fromCenter(
      center: Offset(
        centerX,
        centerY,
      ),
      width: bellyWidth,
      height: bellyHeight,
    );

    canvas.drawOval(
      rect,
      paint,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}

class EyeBallPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final socketWidth = 30.0;
    final socketHeight = socketWidth;

    void paintSocket(double centerX) {
      final centerY = size.height / 3.0;
      final paint = Paint()..color = Colors.white;

      final rect = Rect.fromCenter(
        center: Offset(
          centerX,
          centerY,
        ),
        width: socketWidth,
        height: socketHeight,
      );

      canvas.drawOval(
        rect,
        paint,
      );
    }

    // blue eye sockets

    final centerX = size.width / 2.0;

    paintSocket(centerX - 60.0);
    paintSocket(centerX + 60.0);
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}

enum Leaning { right, left }

class BlackEyeSocketPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final socketWidth = size.width * 0.14;
    final socketHeight = socketWidth * 1.2;

    void paintSocket(double centerX, Leaning leaning) {
      final centerY = size.height / 3.0;
      final paint = Paint()..color = Colors.black;

      final rect = Rect.fromCenter(
        center: Offset(
          centerX,
          centerY,
        ),
        width: socketWidth,
        height: socketHeight,
      );

      canvas.save();

      switch (leaning) {
        case Leaning.left:
          canvas.skew(0.2, 0.0);
          break;
        case Leaning.right:
          canvas.skew(-0.2, 0.0);
          break;
      }

      canvas.drawOval(
        rect,
        paint,
      );

      canvas.restore();
    }

    // blue eye sockets

    final centerX = size.width / 2.0;

    paintSocket(
      centerX - socketWidth / 1.5,
      Leaning.right,
    );
    paintSocket(
      centerX + socketWidth / 1.5,
      Leaning.left,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}

class BlueEyeSocketPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final socketWidth = size.width * 0.35;
    final socketHeight = socketWidth * 1.2;

    void paintSocket(double centerX, Leaning leaning) {
      final centerY = size.height / 3.0;
      final paint = Paint()..color = Colors.blue[400]!;

      final rect = Rect.fromCenter(
        center: Offset(
          centerX,
          centerY,
        ),
        width: socketWidth,
        height: socketHeight,
      );

      canvas.save();

      switch (leaning) {
        case Leaning.left:
          canvas.skew(0.2, 0.0);
          break;
        case Leaning.right:
          canvas.skew(-0.2, 0.0);
          break;
      }

      canvas.drawOval(
        rect,
        paint,
      );

      canvas.restore();
    }

    // blue eye sockets

    final centerX = size.width / 2.0;

    paintSocket(
      centerX - socketWidth / 3.5,
      Leaning.right,
    );
    paintSocket(
      centerX + socketWidth / 3.5,
      Leaning.left,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}

class EarsPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final earWidth = 30.0;

    void drawEar(double centerX) {
      final centerY = size.height / 2.0;
      final earHeight = size.height / 3.0;
      final paint = Paint()..color = Colors.blue[400]!;
      final rect = Rect.fromCenter(
        center: Offset(
          centerX,
          centerY,
        ),
        width: earWidth,
        height: earHeight,
      );
      canvas.drawArc(
        rect,
        0.0,
        pi * 2.0,
        true,
        paint,
      );
    }

    final padding = 5.0;
    drawEar(padding + (earWidth / 2.0));
    drawEar(size.width - ((earWidth / 2.0) + padding));
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}

class HeadPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final paint = Paint()..color = Colors.blue[100]!;
    final center = Offset(
      size.width / 2.0,
      size.height / 2.0,
    );
    canvas.drawCircle(
      center,
      size.width / 2.0,
      paint,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => false;
}

class DashPainter extends CustomPainter {
  final painters = [
    HeadPainter(),
    EarsPainter(),
    BlueEyeSocketPainter(),
    BlackEyeSocketPainter(),
    EyeBallPainter(),
    BellyPainter(),
    NosePainter()
  ];

  @override
  void paint(Canvas canvas, Size size) {
    painters.forEach(
      (p) => p.paint(
        canvas,
        size,
      ),
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) => painters
      .map((p) => p.shouldRepaint(oldDelegate))
      .reduce((p1, p2) => p1 || p2);
}

class Dash extends StatelessWidget {
  const Dash({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return LayoutBuilder(builder: (context, constraints) {
      return Container(
        width: constraints.maxWidth,
        height: constraints.maxWidth,
        child: CustomPaint(
          painter: DashPainter(),
        ),
      );
    });
  }
}

class HomePage extends StatelessWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(child: Dash()),
    );
  }
}
```