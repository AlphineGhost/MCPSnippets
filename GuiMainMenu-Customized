public class GuiMainMenu extends GuiScreen implements GuiYesNoCallback
{
    private static final AtomicInteger field_175373_f = new AtomicInteger(0);
    private static final Logger logger = LogManager.getLogger();

    private GuiButton buttonResetDemo;

    private DynamicTexture viewportTexture;
    private boolean field_175375_v = true;

    private final Object threadLock = new Object();

    private String openGLWarning1;

    private String openGLWarning2;

    private String openGLWarningLink;

    public static final String field_96138_a = "Please click " + EnumChatFormatting.UNDERLINE + "here" + EnumChatFormatting.RESET + " for more information.";
    private int field_92024_r;
    private int field_92023_s;
    private int field_92022_t;
    private int field_92021_u;
    private int field_92020_v;
    private int field_92019_w;

    private GuiButton realmsButton;

    public GuiMainMenu()
    {
        this.openGLWarning2 = field_96138_a;
        BufferedReader bufferedreader = null;

        this.openGLWarning1 = "";

        if (!GLContext.getCapabilities().OpenGL20 && !OpenGlHelper.areShadersSupported())
        {
            this.openGLWarning1 = I18n.format("title.oldgl1", new Object[0]);
            this.openGLWarning2 = I18n.format("title.oldgl2", new Object[0]);
            this.openGLWarningLink = "https://help.mojang.com/customer/portal/articles/325948?ref=game";
        }
    }

    public boolean doesGuiPauseGame()
    {
        return false;
    }

    protected void keyTyped(char typedChar, int keyCode) throws IOException
    {
    }

    public void initGui()
    {
    	AlphaClient.getInstance().getDiscordCore().update("Idle", "Main Menu");
        this.viewportTexture = new DynamicTexture(256, 256);
        Calendar calendar = Calendar.getInstance();
        calendar.setTime(new Date());

        int i = 24;
        int j = this.height / 4 + 48;

        if (this.mc.isDemo())
        {
        }
        else
        {
            this.addSingleplayerMultiplayerButtons(j, 24);
        }

        this.buttonList.add(new GuiButton(20, this.width / 2 - 100, j - 50 + 98, 98, 20, "Alt Login")); //Custom Button for my alt login gui
        this.buttonList.add(new GuiButton(21, this.width / 2 + 2, j - 50 + 98, 98, 20, "Mod Toggle")); //Custom Button for my Toggle Mod gui
        this.buttonList.add(new GuiButton(0, this.width / 2 - 100, j + 72 + 12, 98, 20, I18n.format("MC Options", new Object[0])));
        this.buttonList.add(new GuiButton(4, this.width / 2 + 2, j + 72 + 12, 98, 20, I18n.format("Quit Client", new Object[0])));
//        this.buttonList.add(new GuiButtonLanguage(5, this.width / 2 - 124, j + 72 + 12));

        synchronized (this.threadLock)
        {
            this.field_92023_s = this.fontRendererObj.getStringWidth(this.openGLWarning1);
            this.field_92024_r = this.fontRendererObj.getStringWidth(this.openGLWarning2);
            int k = Math.max(this.field_92023_s, this.field_92024_r);
            this.field_92022_t = (this.width - k) / 2;
            this.field_92021_u = ((GuiButton)this.buttonList.get(0)).yPosition - 24;
            this.field_92020_v = this.field_92022_t + k;
            this.field_92019_w = this.field_92021_u + 24;
        }

        this.mc.func_181537_a(false);
    }

    private void addSingleplayerMultiplayerButtons(int p_73969_1_, int p_73969_2_)
    {
//    	this.buttonList.add(new GuiButton(20, this.width / 2 + 46, p_73969_1_ - 50, 98 + 18 , 20, "Alt Login")); this was a test line
        this.buttonList.add(new GuiButton(1, this.width / 2 - 100, p_73969_1_, I18n.format("menu.singleplayer", new Object[0])));
        this.buttonList.add(new GuiButton(2, this.width / 2 - 100, p_73969_1_ + p_73969_2_ * 1, I18n.format("menu.multiplayer", new Object[0])));
    }

    protected void actionPerformed(GuiButton button) throws IOException
    {
        if (button.id == 0)
        {
            this.mc.displayGuiScreen(new GuiOptions(this, this.mc.gameSettings));
        }

        if (button.id == 5)
        {
            this.mc.displayGuiScreen(new GuiLanguage(this, this.mc.gameSettings, this.mc.getLanguageManager()));
        }

        if (button.id == 1)
        {
            this.mc.displayGuiScreen(new GuiSelectWorld(this));
        }

        if (button.id == 2)
        {
            this.mc.displayGuiScreen(new GuiMultiplayer(this));
        }
        if (button.id == 20)
        {
            this.mc.displayGuiScreen(new GuiAltLogin(this));
        }
        if (button.id == 21)
        {
            this.mc.displayGuiScreen(new GuiModToggle());
        }


        if (button.id == 14 && this.realmsButton.visible)
        {
            this.switchToRealms();
        }

        if (button.id == 4)
        {
            this.mc.shutdown();
        }
    }

    private void switchToRealms()
    {
        RealmsBridge realmsbridge = new RealmsBridge();
        realmsbridge.switchToRealms(this);
    }

    /**
     * Draws the screen and all the components in it. Args : mouseX, mouseY, renderPartialTicks
     */
    public void drawScreen(int mouseX, int mouseY, float partialTicks)
    {
    	GlStateManager.disableAlpha();
        GlStateManager.enableAlpha();
        Tessellator tessellator = Tessellator.getInstance();
        WorldRenderer worldrenderer = tessellator.getWorldRenderer();
        int i = 274;
        int j = this.width / 2 - i / 2;
        int k = 30;
        this.drawGradientRect(0, 0, this.width, this.height, -2130706433, 16777215);
        this.drawGradientRect(0, 0, this.width, this.height, 0, Integer.MIN_VALUE);
        GlStateManager.color(1.0F, 1.0F, 1.0F, 1.0F); 

        //Start of the custom menu background
        ScaledResolution scaledRes = new ScaledResolution(this.mc);
        this.mc.getTextureManager().bindTexture(new ResourceLocation("client/main_background.png"));
        Gui.drawScaledCustomSizeModalRect(0, 0, 0.0F, 0.0F, scaledRes.getScaledWidth(), scaledRes.getScaledHeight(), scaledRes.getScaledWidth(), scaledRes.getScaledHeight(), scaledRes.getScaledWidth(), scaledRes.getScaledHeight());
        //End of the custom menu background
        
        this.drawLogo(); //This draws the custom logo
        
        GlStateManager.pushMatrix();
        GlStateManager.translate((float)(this.width / 2 + 90), 70.0F, 0.0F);
        GlStateManager.rotate(-20.0F, 0.0F, 0.0F, 1.0F);
        float f = 1.8F - MathHelper.abs(MathHelper.sin((float)(Minecraft.getSystemTime() % 1000L) / 1000.0F * (float)Math.PI * 2.0F) * 0.1F);
        f = f * 100.0F / (float)(this.fontRendererObj.getStringWidth("Alpha Rules!") + 32); //This just makes sure the text is sideways
        GlStateManager.scale(f, f, f);
        //Draws the splash text. The RainbowColor class is custom
        this.drawCenteredString(this.fontRendererObj, "Lifetime Alpha!", 0, -8, RainbowColor.rainbowEffect());
        GlStateManager.popMatrix();
        String s = "§e" + AlphaClient.Client_Name + " V" + AlphaClient.Client_Version + "§8 - §eMinecraft §71.8.8";
        String s3 = "§eLogged in as: §7§n";
//        String s4 = "§eDiscord: §7§n"; //Working on a simple Discord Username translator
        this.drawString(this.fontRendererObj, s, 2, this.height - 10, -1);
        this.drawString(this.fontRendererObj, s3, 2, 20, -1);
//        this.drawString(this.fontRendererObj, s4, 2, 32, -1); //This draws the Discord string
        

        String s1 = "Created by: Alphine";
        String s2 = "§7Copyright Mojang AB. Do not distribute!";
        //WaveChroma is a custom class. It can be found in the other user snippets
        WaveChroma.drawChromaString(s1, 1, 3, true);
        this.drawString(this.fontRendererObj, s2, this.width - this.fontRendererObj.getStringWidth(s2) - 2, this.height - 10, -1);
        
        
        if (this.openGLWarning1 != null && this.openGLWarning1.length() > 0)
        {
            drawRect(this.field_92022_t - 2, this.field_92021_u - 2, this.field_92020_v + 2, this.field_92019_w - 1, 1428160512);
            this.drawString(this.fontRendererObj, this.openGLWarning1, this.field_92022_t, this.field_92021_u, -1);
            this.drawString(this.fontRendererObj, this.openGLWarning2, (this.width - this.field_92024_r) / 2, ((GuiButton)this.buttonList.get(0)).yPosition - 12, -1);
        }

        super.drawScreen(mouseX, mouseY, partialTicks);
    }
        
    //Custom Logo using a four point method ;)
    public void drawLogo() {
    	
    	this.mc.getTextureManager().bindTexture(new ResourceLocation("client/MenuSplash.png"));
    	
    	Tessellator tess = Tessellator.getInstance();
    	WorldRenderer wR = tess.getWorldRenderer();
    	
    	wR.begin(7, DefaultVertexFormats.POSITION_TEX);
    	GL11.glTexParameteri(GL11.GL_TEXTURE_2D, GL11.GL_TEXTURE_MIN_FILTER, GL11.GL_LINEAR);
    	GL11.glTexParameteri(GL11.GL_TEXTURE_2D, GL11.GL_TEXTURE_MAG_FILTER, GL11.GL_LINEAR);
    	
    	wR.pos((double)this.width / 2 - 80, (double)0, (double)this.zLevel).tex((double)0, (double)0).endVertex();
    	wR.pos((double)this.width / 2 - 80, (double)this.height / 2 - 8, (double)this.zLevel).tex((double)0, (double)1).endVertex();
    	wR.pos((double)this.width / 2 + 80, (double)this.height / 2 - 8, (double)this.zLevel).tex((double)1, (double)1).endVertex();
    	wR.pos((double)this.width / 2 + 80, (double)0, (double)this.zLevel).tex((double)1, (double)0).endVertex();
        tess.draw();
    }
    

    /**
     * Called when the mouse is clicked. Args : mouseX, mouseY, clickedButton
     */
    protected void mouseClicked(int mouseX, int mouseY, int mouseButton) throws IOException
    {
        super.mouseClicked(mouseX, mouseY, mouseButton);
        Object object = this.threadLock;

        synchronized (this.threadLock)
        {
            if (this.openGLWarning1.length() > 0 && mouseX >= this.field_92022_t && mouseX <= this.field_92020_v && mouseY >= this.field_92021_u && mouseY <= this.field_92019_w)
            {
                GuiConfirmOpenLink guiconfirmopenlink = new GuiConfirmOpenLink(this, this.openGLWarningLink, 13, true);
                guiconfirmopenlink.disableSecurityWarning();
                this.mc.displayGuiScreen(guiconfirmopenlink);
            }
        }
    }
}
