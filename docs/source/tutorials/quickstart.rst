from manim import *

class GapGiayTrungDiem(Scene):
    def construct(self):
        # Cảnh 1
        paper = Rectangle(width=10, height=6, fill_color=WHITE, fill_opacity=0.9)
        self.play(Create(paper))
        A = Dot([-3, 0, 0], color=BLUE)
        B = Dot([3, 0, 0], color=BLUE)
        AB = Line(A.get_center(), B.get_center(), color=BLACK)
        label_A = Tex("A").next_to(A, DOWN)
        label_B = Tex("B").next_to(B, DOWN)
        self.play(Create(AB), Write(label_A), Write(label_B))

        # Cảnh 2: Gấp (giả lập bằng reflection)
        self.wait(1)
        # Giả lập gấp bằng cách reflect A qua crease
        crease = DashedLine([-4, 2, 0], [4, -2, 0], color=RED)  # ví dụ crease
        A_copy = A.copy()
        self.play(A_copy.animate.move_to(B.get_center()), Create(crease), run_time=2)
        self.play(Indicate(A_copy))  # zoom vào trùng khít

        # Cảnh 3: Mở ra, highlight crease
        self.play(FadeOut(A_copy), crease.animate.set_color(RED).set_stroke(width=8))
        self.play(Uncreate(paper))  # giả lập mở
        self.play(Create(paper))   # phẳng lại

        # Cảnh 4
        M = Dot(ORIGIN, color=BLUE, radius=0.15)
        label_M = Tex("M").next_to(M, UP)
        self.play(Create(M), Write(label_M))
        MA = Line(M.get_center(), A.get_center())
        MB = Line(M.get_center(), B.get_center())
        self.play(Create(MA), Create(MB))
        eq = Tex("MA = MB").to_edge(UP, buff=1.5).scale(1.2)
        self.play(Write(eq))
        self.wait(3)
