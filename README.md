if not _G.XYLONOPOINTLOSING then
    _G.XYLONOPOINTLOSING = true
    local StatusIncreaseAmount = 0
    local old
    old = hookmetamethod(game, '__namecall', function(self, ...)
        local args = {...}
        local method = getnamecallmethod()

        if not checkcaller() and method == 'FireServer' and self.Name == "RemoteEvent" and self.Parent.Parent.Parent.Parent.Name == "Status" then
            if args[1] >= 1 and args[1] <= 150 then
                StatusIncreaseAmount = args[1]
            elseif args[1] > 150 then
                StatusIncreaseAmount = 150
            end
            args[1] = 0
            for i = 1, StatusIncreaseAmount do
                old(self, 0.5)
            end
        end

        return old(self, unpack(args))
    end)
end
