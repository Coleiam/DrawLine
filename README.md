# DrawLine
This program draws a line in the screen on a plane from 0 to 100 on X and from 0 to 40 on Y

If someone is interested in the code, see.

using System;
using System.Windows.Input;
using System.IO;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace TestConsole
{
    class Program
    {
        public float x1 = Console.Read();
        public float y1 = Console.Read();
        public float x2 = Console.Read();
        public float y2 = Console.Read();
        static public void Main(string[] args)
        {
            Console.WriteLine("Thick = ");
            float thick1 = Convert.ToSingle(Console.ReadLine());
            Console.WriteLine("X1 = ");
            float x1 = Convert.ToSingle(Console.ReadLine());
            Console.WriteLine("Y1 = ");
            float y1 = Convert.ToSingle(Console.ReadLine());
            Console.WriteLine("X2 = ");
            float x2 = Convert.ToSingle(Console.ReadLine());
            Console.WriteLine("Y2 = ");
            float y2 = Convert.ToSingle(Console.ReadLine());
            int width = 100;
            int height = 40;
            Point[] point = {new Point(x1, y1, ConsoleColor.Blue), new Point(x2, y2, ConsoleColor.Red)};
            for (int j = 0; j <= height; j++)
            {
                for (int i = 0; i <= width; i++)
                {
                    Console.BackgroundColor = ConsoleColor.Black;
                    Draw.DrawLine(i, j, point[0], point[1], thick1);
                    Draw.DrawPoint(i, j, point[0]);
                    Draw.DrawPoint(i, j, point[1]);
                    Console.Write(" .");
                }
                Console.BackgroundColor = ConsoleColor.Black;
                Console.WriteLine("");
            }
            while (true)
            {

            }
        }
    }
    public class Draw
    {
        public static void DrawPoint(int X, int Y, Point point)
        {
            if (point.X == X && point.Y == Y)
            {
                Console.BackgroundColor = point.Color;
            }

        }
        public static void DrawLine(float X, float Y, Point point1, Point point2, float thick)
        {
            Point point = new Point(point1.X - point2.X, point1.Y - point2.Y, ConsoleColor.White);
            Point pointcirle = new Point(((point1.X - point2.X) / 2) + point2.X, ((point1.Y - point2.Y) / 2) + point2.Y, ConsoleColor.White);
            float b = point.X / point.Y;
            float k = point2.X - (point2.Y * b);
            float b1 = point.Y / point.X;
            float k1 = point2.Y - (point2.X * b1);
            if (Y < (X * b1) + k1 + thick && Y > (X * b1) + k1 - thick || X < (Y * b) + k + thick && X > (Y * b) + k - thick)
            {
                float gip1 = (float)Math.Sqrt(Math.Pow((double)pointcirle.X - point2.X, 2) + Math.Pow((double)pointcirle.Y - point2.Y, 2));
                float gip2 = (float)Math.Sqrt(Math.Pow((double)X - pointcirle.X, 2) + Math.Pow((double)Y - pointcirle.Y, 2));
                if (gip2 < gip1 + thick)
                    Console.BackgroundColor = ConsoleColor.White;
            }
        }
    }
    public struct Point
    {
        public Point(float x, float y, ConsoleColor Color_) : this()
        {
            X = x;
            Y = y;
            Color = Color_;
        }
        public float X { get; set; }
        public float Y { get; set; }
        public ConsoleColor Color { get; set; }
    }
}
