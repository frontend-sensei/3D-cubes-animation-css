<template>
  <div class="scene">
    <div class="scene__ground" id="ground">
      <!-- Cubes -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cubes_count: 100,
    };
  },
  mounted() {
    const ground = document.getElementById("ground"),
      cubes_count = this.cubes_count;
    let cube,
      cube_inner = `<div class="cube-center">
            <div class="cube-side cube-side--1"></div>
            <div class="cube-side cube-side--2"></div>
            <div class="cube-side cube-side--3"></div>
            <div class="cube-side cube-side--4"></div>
            <div class="cube-side cube-side--5"></div>
            <div class="cube-side cube-side--6"></div>
        </div>`,
      offsetTop = 0,
      offsetLeft = 0,
      ten_helper = 10;

    // Generation Cubes
    for (let j = 0; j < cubes_count; j++) {
      cube = document.createElement("div");
      cube.className = "cube";
      cube.innerHTML = cube_inner;

      cube.style.top = `${offsetTop}px`;
      cube.style.left = `${offsetLeft}px`;

      ground.appendChild(cube);
      offsetTop += 100;

      if (j > ten_helper && j < ten_helper + 2) {
        offsetTop = 0;
        offsetLeft += 100;
        ten_helper += 10;
      }
    }

    setTimeout(() => {
      document.getElementsByClassName("scene")[0].style.opacity = 1;
      this.initAnimatedCubes();
    }, 1000);
  },

  methods: {
    initAnimatedCubes() {
      const cubes = document.getElementsByClassName("cube");

      for (let j = 0; j < cubes.length / 4; j++) {
        setTimeout(() => {
          const random_el = this.random(0, this.cubes_count - 1),
            random_dur = this.random(5, 10),
            random_del = this.random(2, 6),
            random_animation = this.random(1, 1);

          cubes[
            random_el
          ].style.animation = `${random_dur}s ease-in-out ${random_del}s infinite move-${random_animation}`;
          cubes[random_el]
            .querySelectorAll(".cube-center div")
            .forEach((el) => {
              el.style.animation = `${random_dur}s ease-in-out ${random_del}s infinite blinking-${random_animation}`;
            });
        }, 400);
      }
    },

    random(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min + 1)) + min;
    },
  },
};
</script>
