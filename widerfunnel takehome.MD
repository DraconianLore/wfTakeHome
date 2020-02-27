# 1 - Popup modal
* Control: https://login.getsling.com/register
* View Port: Desktop

``` js
function closeModal() {
  document.getElementById('modal').style = 'display: none';
}
document.querySelector("#content > div > main > signup > div > div > signup-footer > div > p > i > a").onclick = function(e) {
e.preventDefault();

const modalContainer = document.createElement('div');
modalContainer.id = 'modal';
modalContainer.style.cssText = 'position: fixed; top: 0; left: 0; display: flex; align-items: center; justify-content: center; width:100vw; height:100vh; z-index: 999; background-color: rgba(0,0,0,0.5);';
const modal = `
  <div style='width:50vw; height:50vh; border:1px solid #333; border-radius: 5px; background-color: #eee; padding: 20px; display: flex; flex-direction: column; align-items: center; justify-content: space-around;'>
    <p style='color: #0085ff; font-size: 36px; font-weight: 700;'>Welcome to Sling!</p>
    <p style='font-size: 120%;'>Select an option below to get started</p>
    <div style='display: flex; justify-content: space-around; height: 50%;'>
      <div style='display: flex; align-items: center; flex-direction: column; margin: 1em; background-color: #fff;justify-content: center; padding: 1em;'>
      <img src='https://draconianlore.github.io/images/business.png' style='height: 5em; width: 5em; margin-bottom: 1em;'></img>
      <p style='text-align: center;'>I am looking to manage a team with sling</p>
      </div>
      <div style='display: flex; align-items: center; flex-direction: column; margin: 1em; background-color: #fff;justify-content: center; padding: 1em;'>
      <img src='https://draconianlore.github.io/images/group.png' style='height: 5em; width: 5em; margin-bottom: 1em;'></img>
      <p style='text-align: center;'>I am looking to join a team that is using sling</p>
      </div>
    </div>
    <em>Already have an account?<span><a href='/' onClick="closeModal()" > Log In</a></span></em>
  <p onClick="closeModal()" style='padding: 0.3em 0.5em; position: fixed; top: 25vh; right: 25vw; cursor: pointer; color: #000; border-radius: 5px; font-size: 120%; font-weight: 700;' >X</p>
  </div>
`;
modalContainer.innerHTML = modal;
document.body.append(modalContainer)
}
```

------------------------

# 2 - Credit Banner trigger via user scroll
* Control: https://instantink.hpconnected.com/us/en/l/
* View Port: Mobile

``` js
let showBanner = true;
function closeBanner() {
  document.getElementById('banner').style = 'display: none';
  showBanner = false;
}
const banner = document.createElement('div');
banner.style.cssText = 'display: none';
const inner = `<div style='background-color: #0096D6; height: 50px; color: #fff; font-size: 20px; font-weight: 700; display: flex; justify-content: center; align-items: flex-end;'><img src='https://cdn3.iconfinder.com/data/icons/social-messaging-productivity-1-1/128/send-mail-512.png' style='height: 50px; filter: invert(1);'></img><span style='margin: 0 0 8px 8px;'>FREE</span></div>
    <div><p style='border-radius: 50%; border: 1px solid #999; color: #666; float: right; padding: 2px 6px; margin: -10px 1em; cursor: pointer;' onClick='closeBanner()'>X</p>
    <p style='margin: 2vh 15vw;'>Get $10 credit towards your plan and try HP Instant Ink for <strong>FREE</strong> today. No commitments or fees - change or cancel your plan anytime.</p>
    <button style='border-radius: 5px; background-color: #fff; border: 1px solid #0096d6; margin-bottom: 1em; padding: 0.5em 2em; color: #0096d6;'>Get my free link</button>
    </div>`
banner.innerHTML = inner;
banner.id = 'banner';
document.body.append(banner);

const plans = document.getElementById("plans-section").offsetTop;
window.onscroll = function() {if (showBanner) {checkBanner()}};
function checkBanner() {
  if (window.pageYOffset > plans) {
    document.getElementById('banner').style = 'display: block; position: fixed; bottom: 0; width: 100vw; z-index: 99; font-family: "Helvetica Neue",Helvetica,Arial,sans-serif; background-color: #fff;'
  } else {
    document.getElementById('banner').style = 'display: none';
  }
}
```

------------------------

# 3 - Create filter for selecting most suitable plan
* Control: https://envoy.com/pricing/
* View Port: Desktop

``` js
// create 'recommend' banners
recStyle = 'width: 100%; text-align: center; padding: 5px; background-color: #f00; border-radius: 5px 5px 0 0; color: #fff; opacity: 0;';
recInnerText = 'We Recommend';

const bPlan = Array.from(document.querySelectorAll('h3'))
  .find(el => el.textContent === 'Basic');
const bRec = document.createElement('div');
bRec.style = recStyle;
bRec.innerText = recInnerText;
bRec.id = 'recBas';
bPlan.parentElement.parentElement.prepend(bRec);

const sPlan = Array.from(document.querySelectorAll('h3'))
  .find(el => el.textContent === 'Standard');
const sRec = document.createElement('div');
sRec.style = recStyle;
sRec.innerText = recInnerText;
sRec.id = 'recSta';
sPlan.parentElement.parentElement.prepend(sRec);

const pPlan = Array.from(document.querySelectorAll('h3'))
  .find(el => el.textContent === 'Premium');
const pRec = document.createElement('div');
pRec.style = recStyle;
pRec.innerText = recInnerText;
pRec.id = 'recPre';
pPlan.parentElement.parentElement.prepend(pRec);

const ePlan = Array.from(document.querySelectorAll('h3'))
  .find(el => el.textContent === 'Enterprise');
const eRec = document.createElement('div');
eRec.style = recStyle;
eRec.innerText = recInnerText;
eRec.id = 'recEnt';
ePlan.parentElement.parentElement.prepend(eRec);

// create filters
let filters = {
  bp: false,
  lds: false,
  vp: false,
  msf: false,
  vs: false,
  dn: false,
}
function filter(filtered) {
  filters[filtered] = !filters[filtered]
  if (filters[filtered]) {
    document.getElementById(filtered).style.backgroundColor = '#ff6666';
  } else {
    document.getElementById(filtered).style.backgroundColor = '#fff';
  };
  if (filters.bp) {
    document.getElementById('recSta').style.opacity = 1;
  } else {
    document.getElementById('recSta').style.opacity = 0;
  }
  if (filters.vs && filters.dn) {
    document.getElementById('recPre').style.opacity = 1;
    document.getElementById('recSta').style.opacity = 0;
  } else {
    document.getElementById('recPre').style.opacity = 0;
  }
  if (filters.bp && filters.lds && filters.vp && filters.msf && filters.vs && filters.dn) {
    document.getElementById('recEnt').style.opacity = 1;
    document.getElementById('recPre').style.opacity = 0;
    document.getElementById('recSta').style.opacity = 0;
  } else {
    document.getElementById('recEnt').style.opacity = 0;
  }
}

// create filter buttons
const targetSection = document.querySelector('.lg-py6');
const newFilters = document.createElement('div');
newFilters.style = 'height: 200px; width: 100%; margin: 2em 0 -5em 0; display: flex; justify-content: space-around; align-items: center; padding: 0 15vw; text-align: center;';

function createFilters() {
  const filterDetails = [
    {id: 'bp', filterName: 'Badge printing'},
    {id: 'lds', filterName: 'Legal document signing'},
    {id: 'vp', filterName: 'Visitor photos'},
    {id: 'msf', filterName: 'Multiple sign-in flows'},
    {id: 'vs', filterName: 'Visitor screening'},
    {id: 'dn', filterName: 'Delivery notifications'}
  ]
  let htmlString = ``
  for (let fil of filterDetails) {
    htmlString += `<div style='height: 10vw; width: 10vw; background-color: #fff; border-radius: 3px; padding: 0 1vw; cursor: pointer;' onClick="filter('${fil.id}')" id=${fil.id}>
  <img src='https://draconianlore.github.io/images/${fil.id}.png' style='height: 5vw; width: 5vw; margin-top: 1vw;'></img>
  <p style='font-size: 1vw; line-height: 1.2vw;'>${fil.filterName}</p></div>`
  }
  return htmlString;
}
newFilters.innerHTML = createFilters();

targetSection.append(newFilters)
```
