if GetObjectName(GetMyHero()) ~= "Morgana" then return end

require ('Inspired')


local morgana = Menu("Morgana", "Morgana")
morgana:SubMenu("Combo", "Combo")
morgana.Combo:Boolean("Q", "Use Q", true)
morgana.Combo:Boolean("W", "Use W \"don't use, use Misc\"", false)
morgana.Combo:Boolean("R", "Use R at 33% of max life", false)

morgana:SubMenu("Killsteal", "Killsteal")
morgana.Killsteal:Boolean("Q", "with Q", true)
morgana.Killsteal:Boolean("R", "with R \"first damage applied\"", true)

morgana:SubMenu("Kill", "Kill")
morgana.Kill:Boolean("KillCombo", "Kill when possible", true)

morgana:SubMenu("Ult", "UltSettings")
morgana.Ult:Boolean("SmartUlt", "SmartUlt", true)
morgana.Ult:Slider("AutoUlt", "ult at min enemies in range", 2, 1, 5, 1) 
    
 

morgana:SubMenu("Misc", "Misc")
if Ignite ~= nil then morgana.Misc:Boolean("AutoIgnite", "Auto Ignite", true) end
morgana.Misc:Boolean("Wimm", "Use W \"on immobile\"", true)
morgana.Misc:Boolean("AutoE", "use E \"anti cc\"", true)
morgana.Misc:Boolean("SmartZhon", "SmartZhon", true)
morgana.Misc:Slider("AutoZhon", "zhonya if ult at min enemies", 2, 1, 5, 1)
--LoadIOW()

local QRange = GetCastRange(myHero, _Q)
local WRange = GetCastRange(myHero, _W)
local ERange = GetCastRange(myHero, _E)
local RRange = GetCastRange(myHero, _R)
local RName = GetCastName(myHero, _R)

local CCbuffnames = {
"Stun",
"aatroxqknockup",
"CurseoftheSadMummy",
"braumstundebuff",
"caitlynyordletrapdebuff",
"ekkowstun",
"EliseHumanE",
"Pulverize",
"powerfistslow",
"rupturelaunch",
"fiorawstun",
"fizzknockup",
"Taunt",
"gnarstun",
"HowlingGaleSpell",
"jarvanivdragonstrikeph2",
"jinxeminesnare",
"karmaspiritbindroot",
"leblancsoulshacklenet",
"leblancsoulshacklenetm",
"leonazenithbladeroot",
"lissandrawfrozen",
"lulurboom",
"LuxLightBindingMis",
"LuxLightBinding",
"unstoppableforcestun",
"suppression",
"maokaiunstablegrowthroot",
"DarkBindingMissile",
"RyzeW",
"nautilusknockup",
"nautiluspassiveroot",
"reksaiwknockup",
"RengarEFinalMAX",
"sionrtarget",
"sionqknockup",
"sorakaesnare",
"swainshadowgrasproot",
"ThreshQ", 
"threshqfakeknockup",
"varusrroot",
"veigareventhorizonstun",
"virdunkstun",
"yasuorstun",
"yasuorknockupcombo",
"viktorgravitonfieldstun",
"monkeykingspinknockup",
"yasuoQ3mis",
"zyragraspingrootshold",
"zyrabramblezoneknockup",
"xenzhaoknockup",
"root"
}	

local AutoECC = {
["Aatrox"] = {"AatroxQ"},
["Ahri"] = {"AhriSeduce"},
["Alistar"] = {"Pulverize",_W},
["Amumu"] = {"BandageToss","CurseoftheSadMummy"},
["Anivia"] = {"FlashFrostSpell"},
["Annie"] = {_Q,_W,_R},
["Ashe"] = {"EnchantedCrystalArrow"},
["Bard"] = {"BardQ"},
["Braum"] = {"BraumQ", "BraumRWrapper"},
["Blitzcrank"] = {"RocketGrab",_E},
["Brand"] = {_Q, _R},
["Cassiopeia"] = {"CassiopeiaPetrifyingGaze"},
["Chogath"] = {"Rupture"},
["Darius"] = {"DariusAxeGrabCone"},
["Diana"] = {"DianaVortex"},
["Draven"] = {"DravenDoubleShot"},
["Ekko"] = {_W, _R},
["Elise"] = {"EliseHumanE"},
["Ezreal"] = {_R},
["FiddleSticks"] = {"Terrify", _R},
["Fiora"] = {_W},
["Fizz"] = {"FizzMarinerDoom"},
["Galio"] = {"GalioIdolOfDurand"},
["Gnar"] = {"gnarbigw", "GnarR"},
["Gragas"] = {"GragasE", "GragasR"},
["Hecarim"] = {"HecarimUlt"},
["Heimerdinger"] = {"HeimerdingerE"},
["Irelia"] = {"IreliaEquilibriumStrike"},
["Janna"] = {"HowlingGale", _R},
["JarvanIV"] = {"JarvanIVDragonStrike2"},
["Jax"] = {_E},
["Jayce"] = {"JayceThunderingBlow"},
["Jinx"] = {_E},
["Karma"] = {"KarmaW"},
["Katarina"] = {_R},
["Karthus"] = {_W},
["LeBlanc"] = {"LeblancSoulShackle", "LeblancSoulShackleM"},
["LeeSin"] = {"BlindMonkRKick"},
["Leona"] = {_Q, _E, "LeonaSolarFlare"},
["Lissandra"] = {"LissandraW", "LissandraR"},
["Lulu"] = {"LuluW"},
["Lux"] = {"LuxLightBinding", _R},
["Malphite"] = {"UFSlash"},
["Malzahar"] = {"AlZaharNetherGrasp"},
["Maokai"] = {"MaokaiTrunkLine", "MaokaiW"},
["Morgana"] = {"DarkBindingMissile", "SoulShackles"},
["Nami"] = {"NamiQ", "NamiR"},
["Nasus"] = {"NasusW"},
["Nautilus"] = {"NautilusAnchorDrag", "NautilusR"},
["Nocturne"] = {"NocturneUnspeakableHorror"},
["Orianna"] = {_R},
["Pantheon"] = {"PantheonW"},
["Poppy"] = {"PoppyHeroicCharge", _R},
["Rammus"] = {_Q, "PuncturingTaunt"},
["Renekton"] = {_W},
["Rengar"] = {"RengarE"},
["Riven"] = {"RivenMartyr"},
["Ryze"] = {"RyzeW"},
["Sejuani"] = {"SejuaniArcticAssault", "SejuaniGlacialPrisonCast"},
["Shen"] = {"ShenShadowDash"},
["Shyvana"] = {"ShyvanaTransformCast"},
["Singed"] = {"Fling"},
["Sion"] = {_Q, _R},
["Skarner"] = {"SkarnerImpale"},
["Sona"] = {"SonaR"},
["Soraka"] = {_E},
["Swain"] = {"SwainShadowGrasp"},
["Syndra"] = {"SyndraE", _R},
["TahmKench"] = {"TahmKenchQ", "TahmKenchE"},
["Taric"] = {"Dazzle"},
["Thresh"] = {"ThreshQ", "ThreshE", _R},
["Tristana"] = {"TristanaR"},
["TwistedFate"] = {"goldcardpreattack"},
["Urgot"] = {"UrgotR"},
["Varus"] = {"VarusR"},
["Vayne"] = {"VayneCondemn"},
["Veigar"] = {"VeigarEventHorizon"},
["VelKoz"] = {"VelkozE"},
["Vi"] = {"ViQMissile", "ViR"},
["Volibear"] = {_Q},
["Viktor"] = {"ViktorGravitonField", _R},
["Vladimir"] = {_R},
["Warwick"] = {"InfiniteDuress"},
["Wukong"] = {_R},
["Xerath"] = {"XerathMageSpear", _R},
["Yasou"] = {"yasuoq3w"},
["Zac"] = {"ZacE", _R},
["Ziggs"] = {"ZiggsW", _R},
["Zilean"] = {"ZileanQ"},
["Zyra"] = {"ZyraGraspingRoots", "ZyraBrambleZone"}
}


local function CastQ(unit)
	local QPred = GetPredictionForPlayer(GetOrigin(myHero),unit,GetMoveSpeed(unit),1200,300,QRange,100,true,true)
    if QPred.HitChance == 1 then                
        CastSkillShot(_Q,QPred.PredPos)
    end
end	


local function CastW(unit)
	local WPred = GetPredictionForPlayer(GetOrigin(myHero),unit,GetMoveSpeed(unit),999999,0,WRange,350,false,false)
	if WPred.HitChance == 1 then
		CastSkillShot(_W,WPred.PredPos)
	end
end	
	
	
local function CastQAndW(Enemy)
	local QPred = GetPredictionForPlayer(GetOrigin(myHero),Enemy,GetMoveSpeed(Enemy),1200,300,QRange,100,true,true)
	local WPred = GetPredictionForPlayer(GetOrigin(myHero),Enemy,GetMoveSpeed(Enemy),999999,0,WRange,350,false,false)
	if QPred.HitChance == 1 and WPred.HitChance == 1 then
		CastSkillShot(_Q,QPred.PredPos)     
		CastSkillShot(_W,WPred.PredPos)
	end
end

local function CastQAndR(Enemy)
	local QPred = GetPredictionForPlayer(GetOrigin(myHero),Enemy,GetMoveSpeed(Enemy),1200,300,QRange,100,true,true)
	if QPred.HitChance == 1 then
		CastSkillShot(_Q,QPred.PredPos)
		CastTargetSpell(Enemy, _R)
	end
end	



local function CastQWAndR(Enemy)
	local QPred = GetPredictionForPlayer(GetOrigin(myHero),Enemy,GetMoveSpeed(Enemy),1200,300,QRange,100,true,true)
	local WPred = GetPredictionForPlayer(GetOrigin(myHero),Enemy,GetMoveSpeed(Enemy),999999,0,WRange,350,false,false)
	if QPred.HitChance == 1 and WPred.HitChance == 1 then
		CastSkillShot(_Q,QPred.PredPos)     
		CastSkillShot(_W,WPred.PredPos)
		CastTargetSpell(Enemy, _R)
	end
end
	

-- Combo function
local function Combo(unit)
    if IOW:Mode() == "Combo" then
		
		local unit = GetCurrentTarget()
		
		
		-- Just the Q
        if morgana.Combo.Q:Value() and CanUseSpell(myHero, _Q) == READY and ValidTarget(unit, QRange) then
           CastQ(unit) 
        end
		
		
		-- Just the W  *** not recommended instead use Auto w on stun ***
		if morgana.Combo.W:Value() and CanUseSpell(myHero, _W) == READY and ValidTarget(unit, GetCastRange(myHero,_W)) then
			CastW(unit)
		end
		
		
		-- Just the Ult at 33% max health life
        if morgana.Combo.R:Value() and CanUseSpell(myHero, _R) == READY and ValidTarget(unit, RRange) then
            if GetCurrentHP(Enemy) < GetMaxHP(Enemy)/3 then
                CastTargetSpell(Enemy, _R)
            end 
        end
    end
end
	

--  Function SmartUlt Auto ult at X enemies (slider)

local function SmartUlt()
	for _,Enemy in pairs(GetEnemyHeroes()) do
		if morgana.Ult.SmartUlt:Value() and CanUseSpell(myHero, _R) == READY and EnemiesAround(GetOrigin(myHero), RRange-50) >= morgana.Ult.AutoUlt:Value() then
			CastTargetSpell(Enemy, _R)
		end
	end
end
	

	


local function checkCCFunc(Enemy)
	for a=1, 52 do
		local checkCC = GotBuff(Enemy, CCbuffnames[a]) 
		if checkCC ~= 0 then
			CastW(Enemy)
		end
	end
end	
	
	
-- Function auto W when enemy is on hard CC *immobile*   no knockbacks included because the duration is too short
local function AutoW()
	if morgana.Misc.Wimm:Value() and CanUseSpell(myHero, _W) == READY then
		for _,Enemy in pairs(GetEnemyHeroes()) do
			if ValidTarget(Enemy, WRange) then
				checkCCFunc(Enemy)
			end
		end
	end
end






-- KS function
local function KS()
    for _,Enemy in pairs(GetEnemyHeroes()) do
		local EnemyDefStatB = GetCurrentHP(Enemy)+GetDmgShield(Enemy)+GetHPRegen(Enemy)
		local QDmg = (25+55*GetCastLevel(myHero,_Q)+GetBonusAP(myHero)*0.90)
		local RDmg = (95+65*GetCastLevel(myHero,_R)+GetBonusAP(myHero)*0.70)
		
		
		--Q KS
        if morgana.Killsteal.Q:Value() and CanUseSpell(myHero,_Q) == READY and ValidTarget(Enemy,Qrange) and CalcDamage(myHero, Enemy, 0, QDmg) > EnemyDefStatB then
            CastQ(Enemy)
        end 
		
		
        --R KS
        if morgana.Killsteal.R:Value() and CanUseSpell(myHero,_R) == READY and ValidTarget(Enemy,RRange) and CalcDamage(myHero, Enemy, 0, RDmg) > EnemyDefStatB then
            CastTargetSpell(Enemy, _R)
        end
    end
end




-- KillCombo function    
local function KillCombo()
	for _,Enemy in pairs(GetEnemyHeroes()) do
		local EnemyDefStat = GetCurrentHP(Enemy)+GetDmgShield(Enemy)
		local QDmg = (25+55*GetCastLevel(myHero,_Q)+GetBonusAP(myHero)*0.90)
		local RDmg = (95+65*GetCastLevel(myHero,_R)+GetBonusAP(myHero)*0.70)
		local WDmg = (80*GetCastLevel(myHero,_W)+GetBonusAP(myHero)*1.1)        -- **** if he stand on it for the full duration, which the enemy does at lvl 5 binding ****
		local QWDmg = QDmg + WDmg
		local QRDmg = QDmg + RDmg
		local QWRDmg = QDmg + WDmg + RDmg
	
	
		if morgana.Kill.KillCombo:Value() then
			if CanUseSpell(myHero,_Q) == READY and ValidTarget(Enemy,QRange) and CalcDamage(myHero, Enemy, 0, QDmg) > (EnemyDefStat+GetHPRegen(Enemy)) then
				CastQ(Enemy)
			elseif CanUseSpell(myHero,_Q) == READY and ValidTarget(Enemy,QRange) and CanUseSpell(myHero, _W) == READY and ValidTarget(Enemy, WRange) and CalcDamage(myHero, Enemy, 0, QWDmg) > (EnemyDefStat+(GetHPRegen(Enemy)*5)) then
				CastQAndW(Enemy)
			elseif CanUseSpell(myHero,_Q) == READY and ValidTarget(Enemy,QRange) and CanUseSpell(myHero,_R) == READY and ValidTarget(Enemy,RRange) and CalcDamage(myHero, Enemy, 0, QRDmg) > (EnemyDefStat+(GetHPRegen(Enemy)*2)) then
				CastQAndR(Enemy)
			elseif CanUseSpell(myHero,_Q) == READY and ValidTarget(Enemy,QRange) and CanUseSpell(myHero, _W) == READY and ValidTarget(Enemy, WRange) and CanUseSpell(myHero,_R) == READY and ValidTarget(Enemy,RRange) and CalcDamage(myHero, Enemy, 0, QWRDmg) > (EnemyDefStat+(GetHPRegen(Enemy)*5)) then
				CastQWAndR(Enemy)
			end
		end
	end
end
		


			
-- Function auto Ignite
local function AutoIgnite()
    for _,Enemy in pairs(GetEnemyHeroes()) do
        if Ignite and morgana.Misc.AutoIgnite:Value() then
			local EnemyDefStat = GetCurrentHP(Enemy)+GetDmgShield(Enemy)
            if IsReady(Ignite) and 20*GetLevel(myHero)+50 > EnemyDefStat+(GetHPRegen(Enemy)*3) and ValidTarget(Enemy, 600) then
              CastTargetSpell(Enemy, Ignite)
          end
        end 
    end
end
	
	

OnTick(function(myHero)
    if not IsDead(myHero) then
		local unit = GetCurrentTarget()
		KS()
        AutoIgnite()
        Combo(unit)
		AutoW()
		KillCombo()
		SmartUlt()		
    end
end)

OnProcessSpell(function(unit, spellProc)
	if not IsDead(myHero) and morgana.Misc.AutoE:Value() and GetTeam(unit) ~= GetTeam(myHero) and GetObjectType(unit) == Obj_AI_Hero and AutoECC[GetObjectName(unit)] then
		for b,slot in pairs(AutoECC[GetObjectName(unit)]) do
			if slot==spellProc.name then
				if spellProc.name==slot then 
					if (GetDistance(spellProc.endPos,myHero) or GetDistance(spellProc.target, myHero)) < ERange then
						if spellProc.windUpTime > 190 then
							DelayAction(
								function()
									for _,champ in pairs(GetAllyHeroes()) do
										if spellProc.target == champ then
											CastTargetSpell(champ, _E)
										elseif spellProc.target == myHero then
											CastSpell(_E)
										elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) > (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
											CastSpell(_E)
										elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) < (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
											CastTargetSpell(champ, _E)
										elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) == (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
											if GetDistance(spellProc.startPos, champ) > GetDistance(spellProc.startPos, myHero) then
												CastSpell(_E)
											else
												CastTargetSpell(champ, _E)
											end
										end
									end
								end, (spellProc.windUpTime - 190))      --- little humanizer 
						else
							for _,champ in pairs(GetAllyHeroes()) do
								if spellProc.target == champ then
									CastTargetSpell(champ, _E)
								elseif spellProc.target == myHero then
									CastSpell(_E)
								elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) > (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
									CastSpell(_E)
								elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) < (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
									CastTargetSpell(champ, _E)
								elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) == (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
									if GetDistance(spellProc.startPos, champ) > GetDistance(spellProc.startPos, myHero) then
										CastSpell(_E)
									else
										CastTargetSpell(champ, _E)
									end
								end
							end
						end
					end	
				end
			elseif slot==_Q or slot==_W or slot==_E or slot==_R then
				if spellProc.name==GetCastName(unit,slot)then
				
					if (GetDistance(spellProc.endPos,myHero) or GetDistance(spellProc.target, myHero)) < ERange then
						if spellProc.windUpTime > 190 then
							DelayAction(
								function()
									for _,champ in pairs(GetAllyHeroes()) do
										if spellProc.target == champ then
											CastTargetSpell(champ, _E)
										elseif spellProc.target == myHero then
											CastSpell(_E)
										elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) > (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
											CastSpell(_E)
										elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) < (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
											CastTargetSpell(champ, _E)
										elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) == (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
											if GetDistance(spellProc.startPos, champ) > GetDistance(spellProc.startPos, myHero) then
												CastSpell(_E)
											else
												CastTargetSpell(champ, _E)
											end
										end
									end
								end, (spellProc.windUpTime - 190))      --- little humanizer 
						else
							for _,champ in pairs(GetAllyHeroes()) do
								if spellProc.target == champ then
									CastTargetSpell(champ, _E)
								elseif spellProc.target == myHero then
									CastSpell(_E)
								elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) > (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
									CastSpell(_E)
								elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) < (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
									CastTargetSpell(champ, _E)
								elseif (GetDistance(spellProc.endPos, champ)+GetDistance(spellProc.startPos, champ)) == (GetDistance(spellProc.endPos, myHero)+GetDistance(spellProc.startPos, myHero)) then
									if GetDistance(spellProc.startPos, champ) > GetDistance(spellProc.startPos, myHero) then
										CastSpell(_E)
									else
										CastTargetSpell(champ, _E)
									end
								end
							end
						end
					end	
				end
			end
		end			
	end				
end)			



OnProcessSpellComplete(function(myHero, spell)
	if not IsDead(myHero) and morgana.Misc.SmartZhon:Value() and GetItemSlot(myHero, 3157) > 0 and ((GetCurrentHP(myHero) < GetMaxHP(myHero)/2.7) or (EnemiesAround(GetOrigin(myHero), RRange) >= morgana.Misc.AutoZhon:Value())) then
		if spell.name == RName then
			DelayAction(
				function()
					CastSpell(GetItemSlot(myHero, 3157))
				end, 200) -- little humanizer
		end
	end
end)


PrintChat("[InnateSeries] Morgana - Loaded, have fun")
