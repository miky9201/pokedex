<template>
  <div class="details-container">
    <img class="pokeball" src="../assets/pokeball.svg" alt="" />

    <div class="details-header">
      <img
        class="details-icon-arrowback"
        src="../assets/arrow_back.svg"
        alt="arrow-back"
      />
      <h1 class="details-title">Pokemon Name</h1>
      <h2 class="details-number">#999</h2>
    </div>
    <div class="details-pokemon-img">
      <img
        class="details-icon-chevronleft"
        src="../assets/chevron_left.svg"
        alt="chevron-left"
      />
      <img class="silhouette" src="../assets/silhouette.png" alt="" />
      <img
        class="details-icon-chevronright"
        src="../assets/chevron_right.svg"
        alt="chevron-right"
      />
    </div>
    <div class="details-card">
      <div class="details-type-container">
        <div class="details-type">Type</div>
        <div class="details-type">Type</div>
      </div>
      <h2 class="details-subtitle">About</h2>
      <div class="details-attribute">
        <div class="details-frame">
          <div class="details-subframe">
            <img src="../assets/weight.svg" alt="" />
            <p>0,1 kg</p>
          </div>
          <div class="details-info-label">Weight</div>
        </div>
        <div class="hr"></div>
        <div class="details-frame">
          <div class="details-subframe">
            <img src="../assets/straighten.svg" alt="" />
            <p>1,3 m</p>
          </div>
          <div class="details-info-label">Height</div>
        </div>
        <div class="hr"></div>
        <div class="details-frame">
          <div class="details-subframe">
            <p>Levitate</p>
          </div>
          <div class="details-info-label">Moves</div>
        </div>
      </div>
      <div class="description">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc iaculis
        eros vitae tellus condimentum maximus sit amet in eros.
      </div>
      <h2 class="details-subtitle">Base Stats</h2>
      <div class="details-base-stats">
        <div class="details-label-container">
          <div class="details-label">HP</div>
          <div class="details-label">ATK</div>
          <div class="details-label">DEF</div>
          <div class="details-label">SATK</div>
          <div class="details-label">SDEF</div>
          <div class="details-label">SPD</div>
        </div>
        <div class="hr"></div>
        <div class="details-data-container">
          <div class="details-data">999</div>
          <div class="details-data">999</div>
          <div class="details-data">999</div>
          <div class="details-data">999</div>
          <div class="details-data">999</div>
          <div class="details-data">999</div>
        </div>
        <div class="details-chart-container">
          <div id="chart-1" class="details-chart">
            <div class="details-chart-value">
              <div class="details-chart-value-number"></div>
            </div>
          </div>
          <div id="chart-2" class="details-chart">
            <div class="details-chart-value">
              <div class="details-chart-value-number"></div>
            </div>
          </div>
          <div id="chart-3" class="details-chart">
            <div class="details-chart-value">
              <div class="details-chart-value-number"></div>
            </div>
          </div>
          <div id="chart-4" class="details-chart">
            <div class="details-chart-value">
              <div class="details-chart-value-number"></div>
            </div>
          </div>
          <div id="chart-5" class="details-chart">
            <div class="details-chart-value">
              <div class="details-chart-value-number"></div>
            </div>
          </div>
          <div id="chart-6" class="details-chart">
            <div class="details-chart-value">
              <div class="details-chart-value-number"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({});
</script>

<style>
/* Poppins Font */
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

.hr {
  border: none;
  border-left: 1px solid #e0e0e0;
  height: 100%;
  width: 0.0625rem;
  align-self: stretch;
}

.details-container {
  display: flex;
  width: 22.5rem;
  height: 40rem;
  padding: 0.25rem;
  flex-direction: column;
  align-items: flex-start;
  flex-shrink: 0;
  background: var(--Grayscale-Wireframe, #b8b8b8);
}

.pokeball {
  width: 208px;
  height: 208px;
  position: absolute;
  margin: 0.5rem 0.5rem 26.5rem 9rem;
}

.details-icon-arrowback {
  width: 2rem;
  height: 2rem;
}

.details-header {
  width: 19.5rem;
  height: 2rem;
  display: flex;
  padding: 1.25rem 1.25rem 1.5rem 1.25rem;
  align-items: center;
  gap: 0.5rem;
  align-self: stretch;
}

.details-title {
  color: var(--Grayscale-White, #fff);
  /* Header/Headline */
  font-family: Poppins;
  font-size: 1.5rem;
  font-style: normal;
  font-weight: 700;
  line-height: 2rem; /* 133.333% */
  flex: 1 0 0;
}

.details-number {
  color: var(--Grayscale-White, #fff);

  /* Header/Subtitle 2 */
  font-family: Poppins;
  font-size: 0.75rem;
  font-style: normal;
  font-weight: 700;
  line-height: 1rem; /* 133.333% */
}

.details-pokemon-img {
  height: 7rem;
  width: 19.5rem;
  display: flex;
  padding: 1rem 1.25rem;
  margin: 0 0.25rem;
  justify-content: space-between;
  align-items: flex-end;
  flex: 1 0 0;
  align-self: stretch;
}

.details-icon-chevronleft,
.details-icon-chevronright {
  width: 1.5rem;
  height: 1.5rem;
}

.silhouette {
  z-index: 0;
  margin: 0 auto -4.4rem auto;
  display: flex;
  width: 12.5rem;
  height: 12.5rem;
  justify-content: center;
  align-items: center;
  flex-shrink: 0;
}

.details-card {
  display: flex;
  height: 21rem;
  height: 21rem;
  padding: 3.5rem 1.25rem 1.25rem 1.25rem;
  flex-direction: column;
  align-items: flex-start;
  gap: 1rem;
  flex-shrink: 0;
  align-self: stretch;
  border-radius: 0.5rem;
  background: var(--Grayscale-White, #fff);
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.25) inset;
}

.details-type-container {
  height: 1.25rem;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 1rem;
  align-self: stretch;
}

.details-type {
  width: 1.63rem;
  height: 1rem;
  display: flex;
  padding: 0.125rem 0.5rem;
  flex-direction: column;
  align-items: flex-start;
  border-radius: 0.625rem;
  background: var(--Grayscale-Medium, #666);
  color: var(--Grayscale-White, #fff);
  /* Header/Subtitle 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 700;
  line-height: 1rem; /* 160% */
}

.details-subtitle {
  align-self: stretch;
  color: var(--Grayscale-Wireframe, #b8b8b8);
  text-align: center;
  /* Header/Subtitle 1 */
  font-family: Poppins;
  font-size: 0.875rem;
  font-style: normal;
  font-weight: 700;
  line-height: 1rem; /* 114.286% */
}

.details-attribute {
  height: 3rem;
  display: flex;
  align-items: flex-start;
  align-self: stretch;
  background: var(--Grayscale-White, #fff);
}

.details-frame {
  height: 3rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
  flex: 1 0 0;
}

.details-subframe {
  height: 1rem;
  display: flex;
  padding: 0.5rem 0rem;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
  align-self: stretch;
}

.details-subframe p {
  color: var(--Grayscale-Dark, #1d1d1d);
  text-align: justify;

  /* Body/Body 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 400;
  line-height: 1rem; /* 160% */
}

.details-info-label {
  align-self: stretch;
  color: var(--Grayscale-Medium, #666);
  text-align: center;

  /* Body/Caption */
  font-family: Poppins;
  font-size: 0.5rem;
  font-style: normal;
  font-weight: 400;
  line-height: 0.75rem; /* 150% */
}

.description {
  height: 3.75rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  flex: 1 0 0;
  align-self: stretch;
  color: var(--Grayscale-Dark, #1d1d1d);
  text-align: justify;

  /* Body/Body 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 400;
  line-height: 1rem; /* 160% */
}

.details-base-stats {
  height: 6rem;
  display: flex;
  align-items: flex-start;
  gap: 0.5rem;
  align-self: stretch;
  background: var(--Grayscale-White, #fff);
}

.details-label-container {
  width: 1.69rem;
  height: 6rem;
  display: flex;
  padding-right: 0.25rem;
  flex-direction: column;
  align-items: flex-start;
}

.details-label {
  width: 1.6875rem;
  color: var(--Grayscale-Wireframe, #b8b8b8);
  text-align: right;

  /* Header/Subtitle 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 700;
  line-height: 1rem; /* 160% */
}

.details-data-container {
  width: 1.19rem;
  height: 6rem;
  display: flex;
  padding-left: 0.25rem;
  flex-direction: column;
  align-items: flex-start;
}

.details-data {
  width: 1.1875rem;
  color: var(--Grayscale-Dark, #1d1d1d);

  /* Body/Body 3 */
  font-family: Poppins;
  font-size: 0.625rem;
  font-style: normal;
  font-weight: 400;
  line-height: 1rem; /* 160% */
}

.details-chart-container {
  width: 14.6rem;
  height: 6rem;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  flex: 1 0 0;
}

.details-chart {
  width: 14.6rem;
  height: 1rem;
  display: flex;
  height: 1rem;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  gap: -0.25rem;
  align-self: stretch;
}

.details-chart-value {
  width: 14.6rem;
  height: 0.25rem;
  display: flex;
  align-items: flex-start;
  align-self: stretch;
  /* opacity: 0.2; */
  background: var(--Grayscale-Wireframe, #f0f0f0);
  border-radius: 0.25rem;
}

.details-chart-value-number {
  width: 9.56rem;
  height: 0.25rem;

  background: var(--Grayscale-Wireframe, #b8b8b8);
  border-radius: 0.25rem;
}

/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)  
*/

html,
body,
div,
span,
applet,
object,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}
body {
  line-height: 1;
}
ol,
ul {
  list-style: none;
}
blockquote,
q {
  quotes: none;
}
blockquote:before,
blockquote:after,
q:before,
q:after {
  content: "";
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
</style>
