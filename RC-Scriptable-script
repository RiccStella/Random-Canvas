// Scriptable Abstract Art Generator for iOS Widget
const { width, height } = args.widgetParameter 
    ? JSON.parse(args.widgetParameter) 
    : { width: 800, height: 600 }; // Default size if no parameter passed

const canvas = new DrawContext();
canvas.size = new Size(width, height);
canvas.opaque = false;
canvas.respectScreenScale = true;

// Color palette
const palette = ["#d1495b", "#edae49", "#00798c", "#66a182", "#2e4057", "#8d5b4c"];

// Helper functions to create random shapes
function randomColor() {
    return palette[Math.floor(Math.random() * palette.length)];
}

function randomRange(min, max) {
    return Math.random() * (max - min) + min;
}

function drawBackground() {
    canvas.setFillColor(new Color(randomColor()));
    canvas.fill(new Rect(0, 0, width, height));
}

function drawBrushStroke() {
    const color = new Color(randomColor(), randomRange(0.5, 1));
    const x = randomRange(0, width);
    const y = randomRange(0, height);
    const w = randomRange(50, 200);
    const h = randomRange(20, 100);
    const angle = randomRange(0, 360);

    canvas.setFillColor(color);

    // Draw the rotated rectangle manually
    const centerX = x;
    const centerY = y;
    const radianAngle = (angle * Math.PI) / 180;
    const cosA = Math.cos(radianAngle);
    const sinA = Math.sin(radianAngle);

    const corners = [
        { x: -w / 2, y: -h / 2 },
        { x: w / 2, y: -h / 2 },
        { x: w / 2, y: h / 2 },
        { x: -w / 2, y: h / 2 },
    ].map(corner => ({
        x: centerX + corner.x * cosA - corner.y * sinA,
        y: centerY + corner.x * sinA + corner.y * cosA,
    }));

    const path = new Path();
    path.move(new Point(corners[0].x, corners[0].y));
    corners.forEach(corner => path.addLine(new Point(corner.x, corner.y)));
    path.closeSubpath();
    canvas.addPath(path);
    canvas.fillPath();
}

function drawLine() {
    const color = new Color(randomColor(), randomRange(0.5, 1));
    const x1 = randomRange(0, width);
    const y1 = randomRange(0, height);
    const x2 = randomRange(0, width);
    const y2 = randomRange(0, height);
    const lineWidth = randomRange(2, 10);

    canvas.setStrokeColor(color);
    canvas.setLineWidth(lineWidth);

    const path = new Path();
    path.move(new Point(x1, y1));
    path.addLine(new Point(x2, y2));
    canvas.addPath(path);
    canvas.strokePath();
}

function drawSplatter() {
    const color = new Color(randomColor(), randomRange(0.5, 1));
    const x = randomRange(0, width);
    const y = randomRange(0, height);
    const size = randomRange(2, 7);

    canvas.setFillColor(color);
    canvas.fillEllipse(new Rect(x - size / 2, y - size / 2, size, size));
}

function drawCurve() {
    const color = new Color(randomColor(), randomRange(0.5, 1));
    const x1 = randomRange(0, width);
    const y1 = randomRange(0, height);
    const cpX = randomRange(0, width);
    const cpY = randomRange(0, height);
    const x2 = randomRange(0, width);
    const y2 = randomRange(0, height);

    const path = new Path();
    path.move(new Point(x1, y1));
    path.addQuadCurve(new Point(x2, y2), new Point(cpX, cpY));

    canvas.setStrokeColor(color);
    canvas.setLineWidth(3);
    canvas.addPath(path);
    canvas.strokePath();
}

// Generate random abstract art
function generateArt() {
    drawBackground();

    for (let i = 0; i < 10; i++) drawBrushStroke();
    for (let i = 0; i < 10; i++) drawLine();
    for (let i = 0; i < 50; i++) drawSplatter();
    for (let i = 0; i < 5; i++) drawCurve();
}

generateArt();

// Create the widget
const widget = new ListWidget();
widget.backgroundImage = canvas.getImage();
widget.addSpacer();

// Display widget
if (config.runsInWidget) {
    Script.setWidget(widget);
    Script.complete();
} else {
    widget.presentMedium();
}


