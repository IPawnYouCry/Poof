namespace Meepo
{
internal class Program
{
private static Hero me;
private static bool togleW;
private const Key ToggleW = Key.R;


private static void Main(string[] args)
{
Game.OnWndProc += MeepoPoof;
Console.WriteLine("Meepo combo loaded!");
}


private static void MeepoPoof(EventArgs args)
{
if (!Game.IsInGame) return;
me = ObjectMgr.LocalHero;
if (me == null || me.ClassID != ClassID.CDOTA_Unit_Hero_Meepo)
return;
if (!Game.IsChatOpen)
{
{
if (Game.IsKeyDown(ToggleW))
togleW = true;
else
togleW = false;
}
}
var selectedUnit = ObjectMgr.LocalPlayer.Selection.FirstOrDefault();
var meepos = ObjectMgr.GetEntities<Meepo>().Where(meepo => meepo.Team == me.Team && !meepo.Equals(selectedUnit)).ToList();
var target = ObjectMgr.GetEntities<Meepo>().Where(tarMeepo => tarMeepo.Team == me.Team == tarMeepo.Equals(selectedUnit)).ToList();
if (togleW)
{
if (Utils.SleepCheck("Anything"))
{
foreach (var meepo in meepos)
{
foreach (var tarMeepo in target)
{var poof = meepo.Spellbook.SpellW;
poof.UseAbility(tarMeepo);
}


}
Utils.Sleep(150, "Anything");
}
}
}
}
}
